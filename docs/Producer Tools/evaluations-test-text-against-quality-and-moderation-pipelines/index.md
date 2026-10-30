---
title: Self-Service Content Evaluation
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

1. [Comment Quality Pipeline Payload](doc:comment-quality-pipeline)
2. [Comment Moderation Pipeline Payload](doc:copy-of-comment-quality-pipeline-1)
3. [Chat Message Moderation Pipeline Payload](doc:copy-of-comment-quality-pipeline)

## Response

Every response, from every pipeline, has the same five keys:

- `url` : Where to poll this evaluation for result.
- `pipeline` : The pipeline that was run.
- `status` : `pending`, `completed` or `failed`.
- `effective_config` : The final settings used for this evaluation: your saved settings with `override_config` applied. It has the same shape as `override_config` .
- `result` : `null` until `status` is `completed`, then the outcome.
  - `decision` : `pass` or `fail`&#x20;
  - `rules` : A list of rules. One entry per rule. Each rule in the list has 4 keys -
    - `name` : The rule field (quality) or category (moderation)
    - `outcome` : `pass` or `fail` .`error` when a rule couldn't run.
    - `value` : What was measured, e.g. character count, emoji ratio or score
    - `threshold` : The threshold it was compared with.

### Response examples

**Pending (async&#x20;**`POST`**):**

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

**Comment quality(Completed):**

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

**Moderation (Completed):**

```json
{
  "url": "https://<host>/api/v1/applications/<client_id>/evaluations/568811fd-2117-4402-b613-a0d6c96bd527/",
  "pipeline": "comment_moderation",
  "status": "completed",
  "effective_config": {
    "model_id": "unitary/toxic-bert",
    "toxic": 0.8,
    "severe_toxic": 0.8,
    "obscene": 0.8,
    "threat": 0.8,
    "insult": 0.5,
    "identity_hate": 0.8
  },
  "result": {
    "decision": "fail",
    "rules": [
      {"name": "toxic", "outcome": "pass", "value": 0.42, "threshold": 0.8},
      {"name": "severe_toxic", "outcome": "pass", "value": 0.01, "threshold": 0.8},
      {"name": "obscene", "outcome": "pass", "value": 0.05, "threshold": 0.8},
      {"name": "threat", "outcome": "pass", "value": 0.02, "threshold": 0.8},
      {"name": "insult", "outcome": "fail", "value": 0.67, "threshold": 0.5},
      {"name": "identity_hate", "outcome": "pass", "value": 0.01, "threshold": 0.8}
    ]
  }
}
```

<br />

#### **Note:** Results expire **10 minutes** after they're created. After that, the `GET` returns `404`.