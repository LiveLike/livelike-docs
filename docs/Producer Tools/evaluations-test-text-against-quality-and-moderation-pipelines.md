---
title: 'Evaluations: test text against quality and moderation pipelines'
deprecated: false
hidden: true
metadata:
  robots: index
---
Run any text, or an existing comment or chat message, through your application's live **comment quality** or **AI moderation** pipeline and see exactly how it would be scored. Use it to tune rules and thresholds before you save them.

Evaluations are read-only: nothing is saved, and no comment, message or setting is changed.

### Endpoints

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

**Auth:**&#x20;

- A producer access token for the application (`Authorization: Bearer <token>`).&#x20;
- Any other token gets `403`.

### Pipelines

| `pipeline`           | Input (exactly one)    | Max text length | Optional tuning <br />(draft only) |
| -------------------- | ---------------------- | --------------- | ---------------------------------- |
| `comment_quality`    | `text` or `comment_id` | 5000            | `thresholds`                       |
| `comment_moderation` | `text` or `comment_id` | 5000            | `thresholds`                       |
| `chat_moderation`    | `text` or `message_id` | 200             | `thresholds`                       |

### Sync vs async

- **Async (default):** returns `202` with a `url`. Poll that URL until `status` is no longer `pending`.
- **Sync:** send `"async": false` to wait up to about 25 seconds for the result. If it isn't ready in time you get `504` with the same `url`, which you can keep polling.

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