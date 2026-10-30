---
title: Self-Serve Evaluations
excerpt: Test text against quality and moderation pipelines
deprecated: false
hidden: true
metadata:
  robots: index
---
Test any text, or an existing comment or chat message, against your application's **comment quality** and **AI moderation** pipelines and see how each rule scores it.

Evaluations use your saved settings, and you can override them for a single request to try changes before you save them. Evaluations are read-only, they never save or change anything.

## Endpoints

<Table>
  <thead>
    <tr>
      <th style={{ width: "11.1%" }}>
        Method
      </th>

      <th style={{ width: "74.1%" }}>
        Path
      </th>

      <th style={{ width: "15.9%" }}>
        Purpose
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `POST`
      </td>

      <td>
        `/api/v1/applications/{client_id}/evaluations/`
      </td>

      <td>
        Start an evaluation
      </td>
    </tr>

    <tr>
      <td>
        `GET`
      </td>

      <td>
        `/api/v1/applications/{client_id}/evaluations/{evaluation_id}/`
      </td>

      <td>
        Poll the result
      </td>
    </tr>
  </tbody>
</Table>

**Authentication:&#x20;**

- A producer access token for the application (`Authorization: Bearer <token>`)

## Pipelines

| \# | `pipeline`           | What it checks                                                                                            |
| -- | -------------------- | --------------------------------------------------------------------------------------------------------- |
| 1  | `comment_quality`    | Whether a comment qualifies as a quality comment: length, characters, emoji, GIFs, sentiment and toxicity |
| 2  | `comment_moderation` | Whether AI moderation would flag a text or comment                                                        |
| 3  | `chat_moderation`    | Whether AI moderation would flag a text or chat message                                                   |

## Payload

Each pipeline(POST API) needs **exactly one** input:&#x20;

- Either `text`, or the ID of an existing item (e.g Comment ID or Chat message ID).&#x20;
- An optional `override_config` . This changes your saved settings for this request only, fields you leave out keep their saved values. This allows you to evaluate the tuned configuration before saving.

1. &#x20;[Comment Quality pipeline](doc:comment-quality-pipeline)
2. [Comment Moderation pipeline](doc:copy-of-comment-quality-pipeline-1)
3. [Chat Message Moderation pipeline](doc:copy-of-comment-quality-pipeline)

## Response

Every response, from every pipeline, has the same five keys:

| Key                | Description                                                                  |
| ------------------ | ---------------------------------------------------------------------------- |
| `url`              | Where to poll this evaluation.                                               |
| `pipeline`         | The pipeline that was run.                                                   |
| `status`           | `pending`, `completed` or `failed`.                                          |
| `effective_config` | The exact settings used: your saved settings with `override_config` applied. |
| `result`           | `null` until `status` is `completed`, then the outcome (see below).          |

`effective_config` has the same shape as `override_config`:

- **comment_quality pipeline:** the six comment quality rule fields.
- **Moderation pipelines:** `model_id` plus one key per category, with its threshold.

`result` contains:

| Key        | Description                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------- |
| `decision` | `pass` or `fail`. `fail` means at least one rule failed, for moderation, the text would be flagged. |
| `rules`    | One entry per rule (quality) or per category (moderation).                                          |

Each entry in `rules` has:

| Key         | Description                                                                                                     |
| ----------- | --------------------------------------------------------------------------------------------------------------- |
| `name`      | The rule field (quality) or category (moderation).                                                              |
| `outcome`   | `pass` or `fail`. Quality rules can also return `error` when a rule couldn't run; an error counts as a failure. |
| `value`     | What was measured, e.g. character count, emoji ratio or score.                                                  |
| `threshold` | The threshold it was compared with.                                                                             |

#### Response examples

Pending (async `POST`):

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/761a0acd-5fc7-4b35-991e-1c55fc0ad864/",
  "pipeline": "comment_quality",
  "status": "pending",
  "effective_config": {
    "min_char_count": 0,
    "disallowed_chars": "*",
    "emoji_ratio_threshold": 0.7,
    "exclude_gif": false,
    "min_sentiment_score": 0.2,
    "max_toxicity_score": 0.1
  },
  "result": null
}
```

Completed:

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/761a0acd-5fc7-4b35-991e-1c55fc0ad864/",
  "pipeline": "comment_quality",
  "status": "completed",
  "effective_config": {
    "min_char_count": 0,
    "disallowed_chars": "*",
    "emoji_ratio_threshold": 0.7,
    "exclude_gif": false,
    "min_sentiment_score": 0.2,
    "max_toxicity_score": 0.1
  },
  "result": {
    "decision": "pass",
    "rules": [
      {"name": "min_char_count", "outcome": "pass", "value": null, "threshold": 0},
      {"name": "disallowed_chars", "outcome": "pass", "value": "", "threshold": "*"},
      {"name": "emoji_ratio_threshold", "outcome": "pass", "value": 0.0345, "threshold": 0.7},
      {"name": "exclude_gif", "outcome": "pass", "value": null, "threshold": false},
      {"name": "min_sentiment_score", "outcome": "pass", "value": 0.91, "threshold": 0.2},
      {"name": "max_toxicity_score", "outcome": "pass", "value": 0.03, "threshold": 0.1}
    ]
  }
}
```

<br />

<br />

<br />

<br />

Results expire **10 minutes** after they're created. After that, the `GET` returns `404`.

<br />

### Examples

The pipeline examples use `"async": false` so the result comes back in the same response. To get a `url` to poll instead, see [Async: start, then poll](#async-start-then-poll).

#### Comment quality

**Free text**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "comment_quality", "text": "What a finish, great match today!", "async": false}'
```

**Existing comment**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "comment_quality", "comment_id": "<comment-uuid>", "async": false}'
```

**Try draft rules before saving them on free text**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "pipeline": "comment_quality",
        "text": "gg 🔥🔥🔥",
        "override_config": {"min_char_count": 3, "emoji_ratio_threshold": 0.5, "max_toxicity_score": null},
        "async": false
      }'
```

**Try draft rules before saving them on existing comment**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "pipeline": "comment_quality",
        "comment_id": "<comment-uuid>",
        "override_config": {"min_char_count": 3, "emoji_ratio_threshold": 0.5, "max_toxicity_score": null},
        "async": false
      }'
```

#### Comment moderation

**Free text**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "comment_moderation", "text": "<text to test>", "async": false}'
```

**Existing comment**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "comment_moderation", "comment_id": "<comment-uuid>", "async": false}'
```

**Try draft thresholds before saving them&#x20;**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "pipeline": "comment_moderation",
        "text": "<text to test>",
        "override_config": {"insult": 0.5, "threat": 0.3},
        "async": false
      }'
```

#### Chat moderation

**Free text** (max 200 characters)

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "chat_moderation", "text": "<text to test>", "async": false}'
```

**Existing message**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "chat_moderation", "message_id": "<message-uuid>", "async": false}'
```

**Try draft thresholds before saving them**

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "pipeline": "chat_moderation",
        "text": "<text to test>",
        "override_config": {"toxic": 0.6, "obscene": 0.5},
        "async": false
      }'
```

#### Async: start, then poll

Leave out `"async"` (or set it to `true`) and the request returns `202` straight away:

```bash
curl -X POST "$HOST/api/v1/applications/$CLIENT_ID/evaluations/" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"pipeline": "chat_moderation", "text": "<text to test>"}'
```

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/<evaluation_id>/",
  "pipeline": "chat_moderation",
  "status": "pending"
}
```

Poll the `url` until `status` is `completed` or `failed`. Results expire after 10 minutes.

```bash
curl "$HOST/api/v1/applications/$CLIENT_ID/evaluations/<evaluation_id>/" \
  -H "Authorization: Bearer $TOKEN"
```

<br />

### Response

`status` is `pending`, `completed` or `failed`. A completed result has these fields:

| Field              | Meaning                                                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `decision`         | `pass` / `fail` for quality; `allowed` / `flagged` for moderation                                                                   |
| `rules`            | One entry per rule or category: `name`, `outcome` (`pass` / `fail` / `error` / `skipped`), the measured `value` and the `threshold` |
| `effective_config` | The exact config used (saved settings + your overrides)                                                                             |
| `model_id`         | The model(s) that scored the text                                                                                                   |

All quality rules always run, so you see every result, not just the first failure.

**Comment quality**

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/6f1c…/",
  "pipeline": "comment_quality",
  "status": "completed",
  "decision": "fail",
  "effective_config": {
    "min_char_count": 3, "disallowed_chars": "*", "emoji_ratio_threshold": 0.5,
    "exclude_gif": false, "min_sentiment_score": 0.2, "max_toxicity_score": null
  },
  "rules": [
    {"name": "min_char_count", "outcome": "pass", "value": 6, "threshold": 3},
    {"name": "disallowed_chars", "outcome": "pass", "value": null, "threshold": "*"},
    {"name": "emoji_ratio_threshold", "outcome": "fail", "value": 0.6, "threshold": 0.5},
    {"name": "exclude_gif", "outcome": "pass", "value": false, "threshold": false},
    {"name": "min_sentiment_score", "outcome": "pass", "value": 0.71, "threshold": 0.2},
    {"name": "max_toxicity_score", "outcome": "skipped", "value": null, "threshold": null}
  ],
  "model_id": {"min_sentiment_score": "<sentiment-model>", "max_toxicity_score": "<toxicity-model>"}
}
```

**Moderation**

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/9a2e…/",
  "pipeline": "comment_moderation",
  "status": "completed",
  "decision": "flagged",
  "effective_config": {"model_id": "unitary/toxic-bert", "thresholds": {"toxic": 0.8, "insult": 0.5, "threat": 0.3}},
  "rules": [
    {"name": "toxic", "outcome": "pass", "value": 0.42, "threshold": 0.8},
    {"name": "insult", "outcome": "fail", "value": 0.67, "threshold": 0.5},
    {"name": "threat", "outcome": "pass", "value": 0.02, "threshold": 0.3}
  ],
  "model_id": "unitary/toxic-bert"
}
```