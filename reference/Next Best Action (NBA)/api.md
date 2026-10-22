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
| `/health`, `/recommend`  | GET, POST | The earlier recommender, unchanged                             | Live                         |

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

The examples use one illustrative user: a brand-new fan three days after joining. Names and numbers are placeholders.

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
  "client_id": "<client_id>",
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
  "client_id": "<client_id>",
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
  "client_id": "<client_id>",
  "model_version": "v1-2026-10-13",
  "recommended_action_1": "Play Game A – Short description",
  "confidence_score_1": 0.82,
  "why_predicted_1": "They have not played Game A yet. They have not played anything yet, so an easy first game is the quickest win. As a newcomer who has not played yet, a first success matters most. Their churn risk is moderate (0.73), so a timely nudge can keep them engaged. 11% of the 128 users with a similar activity pattern have already done it. It ranked first among the actions open to this user.",
  "what_it_would_do_1": "A quick arcade game that can earn points. Users like them who did this stayed active 64% of the time over the next 14 days. A visit in the next few days would keep their habit from fading.",
  "recommended_game_id_1": "G-<game id A>",
  "recommended_action_2": "Play Game B – Short description",
  "confidence_score_2": 0.16,
  "why_predicted_2": "They have not played Game B yet. They have not played anything yet, so an easy first game is the quickest win. As a newcomer who has not played yet, a first success matters most. 11% of the 128 users with a similar activity pattern have already done it. It is the next-best choice, right behind Game A.",
  "what_it_would_do_2": "Can pay out points. Among similar users who did this, 61% stayed active for the next 14 days. A visit in the next few days would keep their habit from fading.",
  "recommended_game_id_2": "G-<game id B>"
}
```

Each client has its own action list, set in its feature file. The list is returned by `/nba_model_info`.

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
  "client": "<client name>",
  "client_id": "<client_id>",
  "model_version": "v1-2026-10-13",
  "trained_at": "2026-10-13T04:34:59+00:00",
  "feature_groups": { "core": true, "streaks": true, "game_stats": true, "rewards": true, "tiers": true, "quests": false, "leaderboard": false, "comments": false },
  "feature_count": 49,
  "segments": ["high_churn_risk", "never_played_a_game", "…"],
  "actions": ["Play Game A – Short description", "…"],
  "churn_definition": "no engagement event in the next 14 days",
  "metrics": { "model": { "auc": 0.90, "brier": 0.12 }, "old_formula": { "auc": 0.85, "brier": 0.33 } }
}
```

## The models

Each client has its own models, trained only on that client's data and chosen at request time by the API key. Every trained version is saved under `models/<version>/` and `models/latest.txt` points at the live one.

### Churn model

A gradient-boosted classifier (scikit-learn `HistGradientBoostingClassifier`) that predicts the chance a user has no engagement event in the next 14 days. It trains on weekly snapshots of users who were active in the 14 days before each snapshot, and is tested on the most recent snapshot, which the model never saw. Users with no activity in the last 14 days are labelled `lapsed` and are not scored.

Bands are cut from today's active users: the top slice is High, the next is Medium, the rest Low. The cut-offs move a little with each retrain.

Each trained version records these test results in `metrics.json`, and `/nba_model_info` returns them:

| Result        | What it shows                                                                               |
| ------------- | ------------------------------------------------------------------------------------------- |
| Training data | Number of weekly snapshots and rows used                                                    |
| Test set      | The most recent week, held out from training                                                |
| AUC           | How well the score ranks leavers above stayers (1.0 is perfect, 0.5 is a coin flip)         |
| Brier score   | How close the percentages are to what happened (lower is better)                            |
| Baselines     | The same results for an older formula and for recency alone, so the model's lift is visible |
| Band cut-offs | The scores where Medium and High start, taken from today's active users                     |
| Feature count | Number of signals the model reads                                                           |

A client's churn rate can swing between periods, for example after a user spike. That is why bands are quantiles of the current active users and not fixed numbers.

**Signals.** Both models read recency, activity counts over 7, 14 and 28 days, active days, sessions, play and completion counts per game, streaks, reward balance and earnings, days since the last reward, tenure and win rate. Clients with quizzes, predictions or status tiers also get signals from those. The strongest signals are active days in the last 14 to 28 days, days since the last reward and recent event counts.

### User segmentation

Rule-based and multi-label: a user gets every label whose rule they meet, with no clustering. Each rule compares a user's numbers with a threshold saved in `segmentation.joblib`, so the labels stay the same until the next training.

### Next best action

A contextual bandit using Thompson sampling. For each action it learns how often users in a similar situation stayed active over the following 14 days, then draws 300 simulated outcomes per user and ranks actions by how often each came out best (the `confidence_score`).

- **Context.** 12 groups, from recent activity (under 5, 5 to 19, or 20 or more events in 14 days), whether the user has played any game, and whether they joined in the last 21 days.
- **Sparse groups.** Groups with little data are pulled toward the action's overall retention rate (prior strength 20), so one lucky user cannot decide a pick.
- **Adjustments.** Games get a 1.10 boost and an action the user has never done gets a further 1.10. The game they played last is down-weighted to 0.7, so it is not recommended again straight away.
- **Caveat.** The model is observational. It learns from who stayed active after doing an action, not from a randomized test, so users who choose an action may differ from those who do not. Treat the picks as a ranked suggestion, not proof of cause.

Each client has its own action list, defined in its feature file. An action is either an arcade game or a reward action such as answering a quiz, making a prediction, watching a video, joining a chat room or linking an account. Reward actions carry the points they pay out, and one-time actions are offered once.

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

The library versions used for training are recorded in `metrics.json`. The server must run the same versions to load the models.

## Master list of segmentation buckets

Nine buckets, returned in `user_segments` as a comma-separated list. A user can be in several at once, and a user who meets none gets an empty list. The numbers in each rule (shown as N below) are set per client from that client's own users when the model is trained, so the same name can mean a slightly different number for each client.

| Bucket                | Meaning                                | Rule                                                                          |
| --------------------- | -------------------------------------- | ----------------------------------------------------------------------------- |
| `high_churn_risk`     | Likely to go quiet in the next 14 days | Churn score of 0.75 or more                                                   |
| `never_played_a_game` | Has not played any arcade game         | No plays of any game                                                          |
| `game_enthusiast`     | Has played many games                  | N or more games played (about the top quarter of users)                       |
| `high_reward_earner`  | Has earned a lot of points             | N or more points earned in total                                              |
| `new_user`            | Recently joined                        | 21 days or fewer since joining                                                |
| `power_user`          | Very frequent recent activity          | N events and N active days in the last 28 days, both at a high level          |
| `low_activity`        | Established user who is barely active  | N or fewer events in the last 28 days, and joined before the median join date |
| `high_status_tier`    | Reached an upper status tier           | Tier level N or higher (only where the client has tiers)                      |
| `lapsed_user`         | No activity in the last 14 days        | No activity in 14 days                                                        |

- `high_churn_risk` is based on the churn score, so it changes when the model is retrained. Lapsed users have no score and are not placed in it; they get `lapsed_user` instead.
- `lapsed_user` is the only bucket not tied to a per-client number. It is the same 14-day cut-off the churn model uses.
- `low_activity` and `power_user` cannot apply to the same user, and neither can `new_user` and `low_activity`.

### Fan types

Separate from the buckets, each user also belongs to exactly one fan type. It decides the wording of the NBA explanation and is not returned as a field. Fan types are found from each client's own users at training time and named for the behaviour they describe, for example a group of highly engaged regulars, a group of newcomers who have not played, or heavy users who have gone quiet. A client typically has around ten, and `metrics.json` and `explanations.json` record the name, size and average churn score of each.

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