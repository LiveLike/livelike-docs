---
title: Chat Message Moderation pipeline
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: noindex
---
## Payload

| Field             | Type                  | Required                     | Description                                                                                                                             |
| ----------------- | --------------------- | ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `pipeline`        | string                | Yes                          | `"chat_moderation"`                                                                                                                     |
| `text`            | string, max 200 chars | One of `text` / `message_id` | Text to evaluate.                                                                                                                       |
| `message_id`      | UUID                  | One of `text` / `message_id` | A chat message in this application. Its text is evaluated.                                                                              |
| `async`           | boolean               | No (default `true`)          | `true` returns at once with a `url` to poll. `false` waits up to about 25 seconds for the result.                                       |
| `override_config` | object                | No                           | `{category: threshold}`, where each threshold is a number from 0 to 1. A category is flagged when its score is **above** its threshold. |

### Payload examples

```json With Direct Text
{
  "pipeline": "chat_moderation",
  "text": "<text to test>",
  "async": false,
  "override_config": {
    "insult": 0.5,
    "threat": 0.3
  }
}
```
```json With Chat Message ID
{
  "pipeline": "chat_moderation",
  "message_id": "3f6b2c1e-8a4d-4f7e-9b2a-1c5d7e9f0a12",
  "async": false,
  "override_config": {
    "insult": 0.5,
    "threat": 0.3
  }
}
```
