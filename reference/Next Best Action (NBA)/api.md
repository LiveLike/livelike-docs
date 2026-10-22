---
title: NBA API Documentation
excerpt: >-
  Service to scores a client's users for churn risk, segments and the two best
  next actions. The API key decides which client's model runs.
deprecated: false
hidden: false
metadata:
  robots: index
---
**Contents** [Overview](#overview)[Authentication](#auth)[Endpoints](#endpoints) [/predict_churn](#churn)[/predict_user_segments](#segments)[/predict_nba_arcade](#nba)[/save_results](#save)[/jobs/\{job_id\}](#jobs)[/nba_model_info](#info) [The models](#models)[Segmentation buckets](#buckets)[Errors and config](#errors)

# NBA API Documentation

One service scores a client's users for churn risk, segments and the two best next actions. The API key decides which client's model runs.

Updated 2026-10-22. Example values are illustrative; field names and wording templates are real.

## Overview

Every model is trained offline per client, and explanations are written offline too, so no AI call happens when an endpoint is called.

| Endpoint                 | Method    | Returns                                                        | Status                       |
| ------------------------ | --------- | -------------------------------------------------------------- | ---------------------------- |
| `/predict_churn`         | POST      | Churn score, band and reasons per user                         | Live                         |
| `/predict_user_segments` | POST      | Segment labels, history summary and games used                 | Live                         |
| `/predict_nba_arcade`    | POST      | Top 2 next actions with confidence, reason and expected effect | Live                         |
| `/save_results`          | POST      | Saves the all-users result to a Redshift table                 | Planned, not in the code yet |
| `/jobs/{job_id}`         | GET       | Status and results of an all-users scoring job                 | Live                         |
| `/nba_model_info`        | GET       | Model version, training date, signals, actions, test metrics   | Live                         |
| `/health`, `/recommend`  | GET, POST | The earlier PSG recommender, unchanged                         | Live                         |

**Clients live today**

| Client | Client ID                                  | Model version | Signals | Actions |
| ------ | ------------------------------------------ | ------------- | ------- | ------- |
| PSG    | `74tPK1ZegDgUOpNzpalgVXPjRUEi5xje52e3a4Zb` | v1-2026-10-13 | 49      | 8       |
| WWE    | `axQjqQjgwKrPkw8An5TXzwmaCMpVP9RUyPLynCfL` | v2-2026-10-12 | 39      | 6       |

**How a client is chosen.** The `X-API-Key` header holds the application's client secret. The service looks it up in Redshift (`public.application`) to find the client ID, then loads that client's folder and latest model version. Adding a client means adding a folder (`feature_set.json`, `sql/`, `models/<version>/`) with no change to the service code.

## Authentication and request format

Every call needs an `X-API-Key` header. The three prediction endpoints take the same JSON body.

```
curl -X POST https://<host>/predict_churn \
  -H "X-API-Key: <client secret>" \
  -H "Content-Type: application/json" \
  -d '{"user_ids": ["0c1d…", "7a9e…"]}'
```

| Body field      | Type            | Required | Meaning                                                                |
| --------------- | --------------- | -------- | ---------------------------------------------------------------------- |
| `user_ids`      | list of strings | No       | Up to 1,000 user UUIDs. Leave out to score every recently active user. |
| `client_id`     | string          | No       | Must match the client the key belongs to, otherwise 403.               |
| `model_version` | string          | No       | A trained version such as `v1-2026-10-13`. Default is the latest.      |

**Two ways to call**

1. **With&#x20;**`user_ids`**.** Users are scored on the spot from fresh data and the rows come back in the reply.
2. **Without&#x20;**`user_ids`**.** The result for all recently active users is cached for one hour and shared by the three prediction endpoints. If it is ready, it returns at once with `cached: true`. If not, the call returns 202 with a `job_id`, and the job is polled at `/jobs/{job_id}`. "Recently active" means activity in the last 14 days. A user asked for by ID with no activity in that time comes back with band `lapsed` and no churn score; an ID with no data at all is listed in `not_found`.

## Endpoints and example responses

The examples use PSG. The user is a brand-new fan three days after joining.

### Reply envelope

Calls with `user_ids` return this envelope. The same `results` rows appear in cached and job replies.

```
{
  "count": 1,
  "not_found": [],
  "model_version": "v1-2026-10-13",
  "results": [ { "…": "one row per user, fields below" } ],
  "seconds": 2.4
}
```

Every row starts with `prediction_date`, `user_uuid`, `client_id` and `model_version`.

### POST /predict_churn

How likely each user is to have no activity in the next 14 days.

| Field                    | Type           | Meaning                                                                                                  |
| ------------------------ | -------------- | -------------------------------------------------------------------------------------------------------- |
| `days_since_last_active` | number         | Days since the last event.                                                                               |
| `churn_score`            | number or null | 0 to 1 chance of no activity in the next 14 days. Null for lapsed users.                                 |
| `churn_band`             | string         | `low`, `medium`, `high` or `lapsed`. Cut-offs come from the active population, 80th and 50th percentile. |
| `churn_reasons`          | string         | Up to 3 signals that are unusually high or low for this user, in words. Empty when none stands out.      |

```
{
  "prediction_date": "2026-10-22",
  "user_uuid": "a3f1…",
  "client_id": "74tPK1ZegDgUOpNzpalgVXPjRUEi5xje52e3a4Zb",
  "model_version": "v1-2026-10-13",
  "days_since_last_active": 2.0,
  "churn_score": 0.73,
  "churn_band": "medium",
  "churn_reasons": "active days 28d is low (1); events 28d is low (4)"
}
```

A user with no activity in 14 days is not scored:

```
{
  "days_since_last_active": 19.0,
  "churn_score": null,
  "churn_band": "lapsed",
  "churn_reasons": "no activity for 19 days"
}
```

### POST /predict_user_segments

Which segment buckets each user falls in, and a plain-language picture of how they use the app. The full bucket list is in the [master list](#buckets).

| Field                         | Type   | Meaning                                                                                              |
| ----------------------------- | ------ | ---------------------------------------------------------------------------------------------------- |
| `user_segments`               | string | Comma-separated bucket names, in a fixed order. A user can be in several.                            |
| `user_history`                | string | A short summary from the user's own numbers: tenure, recency, trend, games, streak, points and tier. |
| `games_played_events_actions` | string | Games played with counts, games not tried, sessions and events in 14 days, and other actions.        |

```
{
  "prediction_date": "2026-10-22",
  "user_uuid": "a3f1…",
  "client_id": "74tPK1ZegDgUOpNzpalgVXPjRUEi5xje52e3a4Zb",
  "model_version": "v1-2026-10-13",
  "user_segments": "never_played_a_game, new_user",
  "user_history": "A brand-new user in their first days who has not played a game yet and is the most likely to be lost. Joined about 3 days ago. Last active 2 days ago, with 1 active day(s) and 4 events in the last 28 days. Has not played an arcade game yet. Beyond games, has not answered a quiz, has not made a correct prediction. Has not earned any points yet.",
  "games_played_events_actions": "No arcade games played. 1 sessions and 4 events in the last 14 days."
}
```

### POST /predict_nba_arcade

The two best next actions per user, with the reason and what similar users did after the same action. Fields come in pairs, `_1` for the first pick and `_2` for the second.

| Field                         | Type           | Meaning                                                                                                       |
| ----------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------- |
| `recommended_action_1`, `_2`  | string         | The action name from the client's action list.                                                                |
| `confidence_score_1`, `_2`    | number         | Share of 300 simulated draws in which this action ranked best for the user. The two scores need not add to 1. |
| `why_predicted_1`, `_2`       | string         | The reason, built from the user's own numbers and the fan type's pre-written text.                            |
| `what_it_would_do_1`, `_2`    | string         | Expected points and how often similar users stayed active for the next 14 days after the action.              |
| `recommended_game_id_1`, `_2` | string or null | The arcade game to open. Null for quiz and prediction picks.                                                  |

```
{
  "prediction_date": "2026-10-22",
  "user_uuid": "a3f1…",
  "client_id": "74tPK1ZegDgUOpNzpalgVXPjRUEi5xje52e3a4Zb",
  "model_version": "v1-2026-10-13",
  "recommended_action_1": "Play Scratch Card – Scratch to Reveal",
  "confidence_score_1": 0.82,
  "why_predicted_1": "They have not played Scratch Card yet. They have not played anything yet, so an easy first game is the quickest win. As a newcomer who has not played yet, a first success matters most. Their churn risk is moderate (0.73), so a timely nudge can keep them engaged. 11% of the 128 users with a similar activity pattern have already done it. It ranked first among the actions open to this user.",
  "what_it_would_do_1": "A quick arcade game that can earn points. Users like them who did this stayed active 64% of the time over the next 14 days. A visit in the next few days would keep their habit from fading.",
  "recommended_game_id_1": "G-01KGQ39WH2X2Y8X1DJSXGZ08WG",
  "recommended_action_2": "Play Guess What – Quick-Thinking Clue Game",
  "confidence_score_2": 0.16,
  "why_predicted_2": "They have not played Guess What yet. They have not played anything yet, so an easy first game is the quickest win. As a newcomer who has not played yet, a first success matters most. 11% of the 128 users with a similar activity pattern have already done it. It is the next-best choice, right behind Scratch Card.",
  "what_it_would_do_2": "Can pay out points. Among similar users who did this, 61% stayed active for the next 14 days. A visit in the next few days would keep their habit from fading.",
  "recommended_game_id_2": "G-01JSHD62JHF7KD9A6CT570GVTK"
}
```

PSG chooses from 8 actions and WWE from 6; the lists are in [the models](#models).

### POST /save_results Planned

Not in the code yet. The proposal is to write the cached all-users result, with churn, segment and NBA fields joined into one row per user, to a Redshift table named in the request. Each run adds rows stamped with `prediction_date` and `model_version`, so history builds up.

```
{ "table_name": "nba_results" }
```

```
{
  "table": "nba_results",
  "rows_written": 10000,
  "prediction_date": "2026-10-22",
  "model_version": "v1-2026-10-13"
}
```

The table name would accept letters, digits and underscores only. Cost is about $0.05 per run for the write, plus storage.

### GET /jobs/{job_id}

Polls an all-users scoring job started by a call without `user_ids`. Add `?view=churn`, `segments` or `nba_arcade` to pick which fields the rows carry (default `churn`). Jobs are kept in memory on the pod that started them, so poll that pod.

| `status`  | Meaning                                                           |
| --------- | ----------------------------------------------------------------- |
| `running` | Still scoring. Poll again in a minute.                            |
| `done`    | Finished; the reply holds `count`, `model_version` and `results`. |
| `expired` | The one-hour cache lapsed; call the endpoint again.               |
| `failed`  | The job stopped; `error` holds the reason.                        |

First reply to an all-users call (HTTP 202):

```
{
  "job_id": "4eebae02645c",
  "status": "running",
  "poll": "/jobs/4eebae02645c?view=nba_arcade",
  "note": "Scoring all active users. Poll the link, or call this endpoint again in a minute."
}
```

Finished job:

```
{
  "job_id": "4eebae02645c",
  "status": "done",
  "count": 1063,
  "model_version": "v1-2026-10-13",
  "started_at": 1792659600.2,
  "finished_at": 1792659638.9,
  "results": [ { "…": "one row per user" } ]
}
```

### GET /nba_model_info

What model the key's client is running, with its test results.

```
{
  "client": "PSG",
  "client_id": "74tPK1ZegDgUOpNzpalgVXPjRUEi5xje52e3a4Zb",
  "model_version": "v1-2026-10-13",
  "trained_at": "2026-10-13T04:34:59+00:00",
  "feature_groups": { "core": true, "streaks": true, "game_stats": true, "rewards": true, "tiers": true, "quests": false, "leaderboard": false, "comments": false },
  "feature_count": 49,
  "segments": ["high_churn_risk", "never_played_a_game", "…"],
  "actions": ["Play Spin the Wheel – Fast-Paced Game of Chance", "…"],
  "churn_definition": "no engagement event in the next 14 days",
  "metrics": { "model": { "auc": 0.90, "brier": 0.12 }, "old_formula": { "auc": 0.85, "brier": 0.33 } }
}
```

## The models

Each client has its own models, trained only on that client's data and chosen at request time by the API key. Every trained version is saved under `models/<version>/` and `models/latest.txt` points at the live one.

### Churn model

A gradient-boosted classifier (scikit-learn `HistGradientBoostingClassifier`) that predicts the chance a user has no engagement event in the next 14 days. It trains on weekly snapshots of users who were active in the 14 days before each snapshot, and is tested on the most recent snapshot, which the model never saw. Users with no activity in the last 14 days are labelled `lapsed` and are not scored.

Bands are cut from today's active users: the top slice is High, the next is Medium, the rest Low. The cut-offs move a little with each retrain.

|                                      | PSG (v1-2026-10-13)            | WWE (v2-2026-10-12)            |
| ------------------------------------ | ------------------------------ | ------------------------------ |
| Training data                        | 7 weekly snapshots, 9,614 rows | 6 weekly snapshots, 5,609 rows |
| Test set (last week)                 | 1,292 users                    | 954 users                      |
| AUC, model                           | 0.90                           | 0.86                           |
| AUC, old formula                     | 0.85                           | 0.79                           |
| AUC, recency only                    | 0.81                           | 0.76                           |
| Brier score, model (lower is better) | 0.12                           | 0.17                           |
| Brier score, old formula             | 0.33                           | 0.33                           |
| High band starts at score            | 0.91                           | 0.78                           |
| Medium band starts at score          | 0.71                           | 0.41                           |
| Features used                        | 49                             | 39                             |

AUC is how well the score ranks leavers above stayers (1.0 is perfect, 0.5 is a coin flip). The Brier score measures how close the percentages are to what happened, so it matters when the score is read as a probability.

PSG scores shift with the period: its churn rate swung from 85% in mid-August, after a user spike, to 49 to 64% in September. That is why bands are quantiles of the current active users.

**Signals.** Both models read recency, activity counts over 7, 14 and 28 days, active days, sessions, play and completion counts per game, streaks, reward balance and earnings, days since the last reward, tenure and win rate. PSG also uses quiz and prediction counts and tier. The strongest signals are active days in the last 14 to 28 days, days since the last reward and recent event counts.

### User segmentation

Rule-based and multi-label: a user gets every label whose rule they meet, with no clustering. Each rule compares a user's numbers with a threshold saved in `segmentation.joblib`, so the labels stay the same until the next training.

### Next best action

A contextual bandit using Thompson sampling. For each action it learns how often users in a similar situation stayed active over the following 14 days, then draws 300 simulated outcomes per user and ranks actions by how often each came out best (the `confidence_score`).

- **Context.** 12 groups, from recent activity (under 5, 5 to 19, or 20 or more events in 14 days), whether the user has played any game, and whether they joined in the last 21 days.
- **Sparse groups.** Groups with little data are pulled toward the action's overall retention rate (prior strength 20), so one lucky user cannot decide a pick.
- **Adjustments.** Games get a 1.10 boost and an action the user has never done gets a further 1.10. The game they played last is down-weighted to 0.7, so it is not recommended again straight away.
- **Caveat.** The model is observational. It learns from who stayed active after doing an action, not from a randomized test, so users who choose an action may differ from those who do not. Treat the picks as a ranked suggestion, not proof of cause.

| Client  | Actions the model chooses from                                                                                                                      |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| PSG (8) | Spin the Wheel, Guess the Word, Guess the Image, Pick Your Team, Guess What, Scratch Card, Answer a quiz (8 points), Make a prediction (108 points) |
| WWE (6) | Guess the Word (10 points), Guess the Image (10), Trivia (10), Watch a VOD (50), Join a chat room (30), Connect Fanatics (250, one time)            |

### Explanations

No AI call is made when a request arrives. The explanation text is prepared when the model is trained:

1. Users are grouped into **fan types** (archetypes) with a small decision tree, each with a name and a size.
2. Claude writes the wording for each fan type and action once, offline, and it is saved in `explanations.json`.
3. At request time the API picks the fan type, then fills the text with the user's own numbers: churn score, the share of similar users who did the action, and the retention of those who did.

This keeps replies fast, cheap and the same every time for the same inputs.

### Training and versioning

Training runs per client and writes a new version folder. The API reads `latest.txt`, so a new version goes live by updating that one file, and an older version can be restored by pointing it back.

| File in `models/<version>/` | What it holds                                                                       |
| --------------------------- | ----------------------------------------------------------------------------------- |
| `churn_model.joblib`        | The trained churn classifier and its feature list                                   |
| `segmentation.joblib`       | The thresholds for the segment rules                                                |
| `explainer.joblib`          | The decision tree that assigns fan types                                            |
| `explanations.json`         | Fan-type names and the pre-written text fragments                                   |
| `nba_bandit.json`           | Retention counts per context and action, prior strength, game boost                 |
| `metrics.json`              | Training data summary, test results, band cut-offs, segment sizes, library versions |

Both current versions were built with scikit-learn 1.9.1, pandas 3.0.5 and numpy 2.5.3. The server must run the same versions to load them.

## Master list of segmentation buckets

Nine buckets, returned in `user_segments` as a comma-separated list. A user can be in several at once, and a user who meets none gets an empty list. Thresholds are set per client from that client's own users when the model is trained. Sizes are for the current model, out of 1,063 active PSG users and 2,029 active WWE users.

| Bucket                | Meaning                                | PSG rule                                                          | WWE rule                                                           | PSG users   | WWE users   |
| --------------------- | -------------------------------------- | ----------------------------------------------------------------- | ------------------------------------------------------------------ | ----------- | ----------- |
| `high_churn_risk`     | Likely to go quiet in the next 14 days | Churn score 0.75 or more                                          | Churn score 0.75 or more                                           | 494         | 496         |
| `never_played_a_game` | Has not played any arcade game         | No plays of any game                                              | No plays of any game                                               | 33          | 9           |
| `game_enthusiast`     | Has played many games                  | 10 or more games played                                           | 33 or more games played                                            | 277         | 512         |
| `high_reward_earner`  | Has earned a lot of points             | 2,524 or more points earned in total                              | 4,630 or more points earned in total                               | 266         | 508         |
| `new_user`            | Recently joined                        | 21 days or fewer since joining                                    | 21 days or fewer since joining                                     | 384         | 282         |
| `power_user`          | Very frequent recent activity          | 70 or more events and 6 or more active days in the last 28 days   | 79 or more events and 11 or more active days in the last 28 days   | 242         | 439         |
| `low_activity`        | Established user who is barely active  | 7 or fewer events in the last 28 days, joined 91 or more days ago | 11 or fewer events in the last 28 days, joined 72 or more days ago | 73          | 201         |
| `high_status_tier`    | Reached an upper status tier           | Tier level 2 or higher                                            | Tier level 3 or higher                                             | 27          | 211         |
| `lapsed_user`         | No activity in the last 14 days        | No activity in 14 days                                            | No activity in 14 days                                             | not counted | not counted |

- `high_churn_risk` is based on the churn score, so it changes when the model is retrained. Lapsed users have no score and are not placed in it; they get `lapsed_user` instead.
- `lapsed_user` is the only bucket not tied to a per-client threshold. It is the same 14-day cut-off the churn model uses.
- `low_activity` and `power_user` cannot apply to the same user, and neither can `new_user` and `low_activity`.
- A badge collector bucket was planned but is not computed for WWE, because no badge assignments were found for it.

### Fan types

Separate from the buckets, each user also belongs to exactly one fan type. It decides the wording of the NBA explanation and is not returned as a field. The average churn score is across active users of that type.

| PSG fan type                   | Users | Avg churn score |
| ------------------------------ | ----- | --------------- |
| One-visit newcomers gone quiet | 342   | 0.91            |
| Highly engaged regulars        | 242   | 0.02            |
| Brand-new users                | 128   | 0.80            |
| Veterans, light now            | 64    | 0.71            |
| Heavy users gone quiet         | 62    | 0.35            |
| Cooling players                | 52    | 0.42            |
| Newcomers testing the app      | 52    | 0.79            |
| Occasional players             | 41    | 0.60            |
| Active but irregular           | 40    | 0.20            |
| Veterans slipping away         | 40    | 0.58            |

| WWE fan type                | Users | Avg churn score |
| --------------------------- | ----- | --------------- |
| Highly engaged regulars     | 537   | 0.03            |
| Light players fading        | 290   | 0.70            |
| One-day visitors            | 259   | 0.81            |
| Occasional players          | 223   | 0.38            |
| Occasional players slipping | 168   | 0.54            |
| Steady regulars             | 156   | 0.21            |
| Newcomers yet to play       | 128   | 0.88            |
| Newcomers who tried a game  | 95    | 0.70            |
| Heavy users gone quiet      | 91    | 0.17            |
| Cooling players             | 82    | 0.31            |

## Errors, limits and configuration

Errors come back as JSON with a `detail` message.

| Code | When                                                                  | `detail` (shortened)                                            |
| ---- | --------------------------------------------------------------------- | --------------------------------------------------------------- |
| 400  | `user_ids` is an empty list                                           | user_ids is empty; omit it to score all active users            |
| 400  | More than 1,000 `user_ids`                                            | At most 1000 user_ids per call; omit user_ids to score everyone |
| 400  | `view` on `/jobs/{job_id}` is not `churn`, `segments` or `nba_arcade` | view must be one of \[...]                                      |
| 403  | No `X-API-Key` header                                                 | Missing X-API-Key header                                        |
| 403  | Key not recognised                                                    | Invalid API key                                                 |
| 403  | A `client_id` is sent that does not belong to the key                 | API key does not belong to this client_id                       |
| 404  | The client has no model folder or no trained version                  | No NBA model is set up for this client                          |
| 404  | `job_id` unknown, for example after a restart                         | Unknown job                                                     |
| 500  | The client's `feature_set.json` does not match the saved model        | feature_set.json does not match the saved model's features      |
| 502  | Scoring failed, for example a data pull error                         | Prediction failed: ...                                          |
| 503  | The key lookup could not be reached                                   | Auth service unavailable                                        |

A user asked for by ID with no data goes in `not_found`; that is not an error.

### Limits

| Limit                           | Value                                                  |
| ------------------------------- | ------------------------------------------------------ |
| `user_ids` per call             | 1,000                                                  |
| All-users result cache          | 1 hour, shared by the churn, segment and NBA endpoints |
| Key lookup cache                | 5 minutes                                              |
| Draws per user in the NBA model | 300                                                    |
| Job storage                     | In memory, so a job is lost if its pod restarts        |

An all-users call within an hour of the last one returns the stored result (`cached: true`) without a new data pull. A key added or removed can take up to five minutes to take effect.

### Configuration

Set as environment variables on the service. Adding a client needs none of them.

| Variable                                                  | Default              | Purpose                                           |
| --------------------------------------------------------- | -------------------- | ------------------------------------------------- |
| `NBA_V2_MAX_USERS`                                        | 1000                 | Most `user_ids` accepted per call                 |
| `NBA_POP_TTL`                                             | 3600                 | Seconds the all-users result is kept              |
| `NBA_ROOT`                                                | the service folder   | Where the client folders are found                |
| `AUTH_APPLICATION_TABLE`                                  | `public.application` | Redshift table the API keys are looked up in      |
| `REDSHIFT_HOST`, `_PORT`, `_DBNAME`, `_USER`, `_PASSWORD` | none                 | Redshift connection for data pulls and key lookup |
| `POSTGRES_HOST`, `_PORT`, `_DBNAME`, `_USER`, `_PASSWORD` | none                 | Optional; tier data where a client has it         |

Credentials belong in the service's environment, never in a request or in the client folders.

### Adding a client

Create a folder named with the client's ID containing `feature_set.json`, a `sql/` folder, and `models/<version>/` with `models/latest.txt`. The service finds it at the next request, and the `X-API-Key` of that client's application selects it. No code changes are needed.
