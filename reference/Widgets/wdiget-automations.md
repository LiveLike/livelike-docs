---
title: Widget Automations
excerpt: >-
  Create automation partners that publish widgets automatically from live sports
  event data.
deprecated: false
hidden: false
metadata:
  robots: index
---
Use live-action automation partners to connect a sports event, identified by `event_id`, to automated widget-publishing rules. When the partner reports a tracked event, such as a goal, try, or match start, the automation publishes the configured widget to the linked programme.

***

# Base URL

```
/{version}/automation-partners/
```

`version` is currently `v1`.

***

# Authentication

All endpoints require a **Bearer token**. Refer to the [authentication](doc:authentication) documentation to generate and send access tokens.

```
Authorization: Bearer <access_token>
```

***

# Endpoints

| Method   | Path                            | Description                              |
| -------- | ------------------------------- | ---------------------------------------- |
| `GET`    | `/v1/automation-partners/`      | List automation partners                 |
| `POST`   | `/v1/automation-partners/`      | Create an automation partner             |
| `GET`    | `/v1/automation-partners/{id}/` | Retrieve an automation partner           |
| `PUT`    | `/v1/automation-partners/{id}/` | Full update (replaces automated actions) |
| `DELETE` | `/v1/automation-partners/{id}/` | Delete an automation partner             |

> ⚠️ Use `PUT` for all updates. `PATCH` is not supported.

***

# Query Parameters (GET list)

| Parameter    | Type   | Required | Description                                                                                               |
| ------------ | ------ | -------- | --------------------------------------------------------------------------------------------------------- |
| `client_id`  | string | **Yes**  | Filter by application `client_id`                                                                         |
| `program_id` | UUID   | No       | Filter by programme UUID                                                                                  |
| `ordering`   | string | No       | One of `match_scheduled_at`, `status`, `automation_status`, `created_at`. Prefix with `-` for descending. |

***

# Event Category, Subcategory and Partner Type

The `event_category` + `event_subcategory` pair identifies the event type and determines which `partner_type` values you can use. Omit `partner_type` to use the default partner for the combination. If you provide `partner_type`, use one of the supported values for that combination.

Each category/subcategory combination supports one or more partners. New integrations may add more `partner_type` values to an existing combination.

| `event_category` | `event_subcategory` | Supported `partner_type` values | Description                                   |
| ---------------- | ------------------- | ------------------------------- | --------------------------------------------- |
| `sports`         | `football`          | `statsperform`                  | Football (association football) match actions |
| `sports`         | `rugby`             | `opta`                          | Rugby union match actions                     |

**Validation rules:**

- Both `event_category` and `event_subcategory` are **required**.
- `event_subcategory` cannot be provided without `event_category`.
- The combination must be one of the recognised pairs in the table above.
- If `partner_type` is provided, it must be one of the supported values for the given combination.

***

# Request Payload

## Top-level fields

| Field                | Type              | Required | Description                                                                                                            |
| -------------------- | ----------------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| `event_id`           | string            | **Yes**  | Partner-specific event/match identifier (e.g. `"srm:match:football-test-001"`)                                         |
| `event_category`     | string            | **Yes**  | Event category — currently always `"sports"`                                                                           |
| `event_subcategory`  | string            | **Yes**  | Event subcategory — see table above                                                                                    |
| `program_id`         | UUID              | **Yes**  | UUID of the programme that owns this partner                                                                           |
| `automated_actions`  | array             | **Yes**  | Action configurations. Provide at least 1 item                                                                         |
| `partner_type`       | string            | No       | Override the partner type — must be a supported value for the given `event_category` / `event_subcategory` combination |
| `match_scheduled_at` | ISO 8601 datetime | No       | Scheduled match or event start time                                                                                    |
| `widget_timeout`     | ISO 8601 duration | No       | How long automated widgets stay active (default: `"PT15S"`)                                                            |
| `widget_title`       | string            | No       | Default title for automated widgets                                                                                    |
| `status`             | boolean           | No       | Enables or disables the automation partner (default: `false`)                                                          |
| `sponsor_ids`        | array of UUIDs    | No       | Sponsors to attach to published widgets                                                                                |

***

# `automated_actions` array

Use each element to configure one action trigger. All widgets within an action must use the same `widget_kind`.

| Field              | Type              | Required | Description                                                                                                            |
| ------------------ | ----------------- | -------- | ---------------------------------------------------------------------------------------------------------------------- |
| `action_type`      | string            | **Yes**  | Action type constant — see [Football Action Types](#football-action-types) / [Rugby Action Types](#rugby-action-types) |
| `enabled`          | boolean           | No       | Enables or disables the action (default: `true`)                                                                       |
| `widgets`          | array             | **Yes**  | Widget variants for this action — minimum 1, maximum 5                                                                 |
| `publish_delay`    | ISO 8601 duration | No       | Delay before publishing after the event fires (default: `"PT0S"`)                                                      |
| `max_widgets`      | integer           | No       | Maximum number of widgets published per match for this action                                                          |
| `cooldown_minutes` | integer           | No       | Minimum minutes between consecutive publishes of this action                                                           |

***

# `widgets` array

Use each element to define one widget variant. Each action can include up to 5 widgets. The automation randomly selects one variant when it publishes the action.

> 📘 Create v/s Update
>
> **Create** — omit `widget_id` to create a new template.
>
> **Update** — provide `widget_id` to update an existing template in-place. Templates whose `widget_id` is absent from the `PUT` body are deleted.

| Field         | Type   | Required | Description                                        |
| ------------- | ------ | -------- | -------------------------------------------------- |
| `widget_kind` | string | **Yes**  | One of `"text-poll"`, `"alert"`, `"emoji-slider"`  |
| `widget_id`   | UUID   | No       | ID of an existing template to update (update only) |
| `payload`     | object | **Yes**  | Widget-specific content — see below                |

***

# Widget Payload Structures

## text-poll

Use `text-poll` to present a multiple-choice question to viewers.

```json
{
  "widget_kind": "text-poll",
  "payload": {
    "question": "Who scored the goal?",
    "options": [
      { "description": "Player A" },
      { "description": "Player B" }
    ],
    "timeout": "PT30S",
    "custom_data": "{\"key\": \"value\"}",
    "localized_data": {
      "fr": {
        "question": "Qui a marqué le but ?",
        "options": [
          { "description": "Joueur A" },
          { "description": "Joueur B" }
        ]
      },
      "es": {
        "question": "¿Quién marcó el gol?",
        "options": [
          { "description": "Jugador A" },
          { "description": "Jugador B" }
        ]
      }
    }
  }
}
```

| Field            | Type              | Required | Description                                                                                                      |
| ---------------- | ----------------- | -------- | ---------------------------------------------------------------------------------------------------------------- |
| `question`       | string            | **Yes**  | The poll question text. Supports `{{variableName}}` placeholders — see [Template Variables](#template-variables) |
| `options`        | array             | **Yes**  | Answer options — each with a `"description"` string                                                              |
| `timeout`        | ISO 8601 duration | No       | How long the poll accepts votes                                                                                  |
| `custom_data`    | string (JSON)     | No       | Arbitrary JSON string attached to the widget                                                                     |
| `localized_data` | object            | No       | BCP-47 locale keys mapping to translated `question` and `options`                                                |

***

## alert

Use `alert` to publish a notification card to viewers.

```json
{
  "widget_kind": "alert",
  "payload": {
    "text": "⚽ GOAL! {{goalScorer}} scores for {{teamDescription}}!",
    "title": "Goal!",
    "image_url": "https://cdn.example.com/goal.png",
    "link_url": "https://example.com/match-centre",
    "link_label": "View match centre",
    "timeout": "PT15S",
    "custom_data": null,
    "localized_data": {
      "fr": {
        "title": "But !",
        "text": "⚽ BUT ! {{goalScorer}} marque pour {{teamDescription}} !",
        "link_label": "Voir le centre de match"
      }
    }
  }
}
```

| Field            | Type              | Required | Description                                                            |
| ---------------- | ----------------- | -------- | ---------------------------------------------------------------------- |
| `text`           | string            | **Yes**  | Alert body text. Supports `{{variableName}}` placeholders              |
| `title`          | string            | No       | Alert heading (max 500 characters)                                     |
| `image_url`      | URL               | No       | Image shown on the alert card                                          |
| `link_url`       | URL               | No       | Call-to-action URL                                                     |
| `link_label`     | string            | No       | Label for the call-to-action link                                      |
| `timeout`        | ISO 8601 duration | No       | How long the alert is visible                                          |
| `custom_data`    | string (JSON)     | No       | Arbitrary JSON string attached to the widget                           |
| `localized_data` | object            | No       | BCP-47 locale keys mapping to translated `title`, `text`, `link_label` |

***

## emoji-slider

Use `emoji-slider` to present an emoji reaction slider to viewers.

```json
{
  "widget_kind": "emoji-slider",
  "payload": {
    "question": "Rate that goal! 🔥",
    "options": [
      { "image_url": "https://cdn.example.com/fire.png" },
      { "image_url": "https://cdn.example.com/meh.png" }
    ],
    "initial_magnitude": 0.5,
    "timeout": "PT20S",
    "custom_data": null,
    "localized_data": {
      "de": {
        "question": "Bewerte dieses Tor! 🔥"
      }
    }
  }
}
```

| Field               | Type              | Required | Description                                                         |
| ------------------- | ----------------- | -------- | ------------------------------------------------------------------- |
| `question`          | string            | **Yes**  | The slider question/label. Supports `{{variableName}}` placeholders |
| `options`           | array             | **Yes**  | Emoji options — each with an `"image_url"` string                   |
| `initial_magnitude` | decimal (0.0–1.0) | No       | Starting position of the slider (default: `0.5`)                    |
| `timeout`           | ISO 8601 duration | No       | How long the slider accepts responses                               |
| `custom_data`       | string (JSON)     | No       | Arbitrary JSON string attached to the widget                        |
| `localized_data`    | object            | No       | BCP-47 locale keys mapping to translated `question`                 |

***

# Template Variables

Widget text fields support `{{variableName}}` placeholders. The automation replaces each placeholder with live event data at publish time. Available variables depend on the action type.

## Football template variables

| Action type      | Available variables                                                  |
| ---------------- | -------------------------------------------------------------------- |
| `match_start`    | `{{teamDescription}}`                                                |
| `goal`           | `{{goalScorer}}`                                                     |
| `shot`           | `{{playerShot}}`                                                     |
| `yellow_card`    | `{{cardType}}`, `{{playerName}}`, `{{cardReason}}`                   |
| `red_card`       | `{{cardType}}`, `{{playerName}}`, `{{cardReason}}`                   |
| `substitution`   | `{{playerOffName}}`, `{{playerOnName}}`                              |
| `missed_penalty` | `{{playerMissedPenalty}}`                                            |
| `var_event`      | `{{varType}}`, `{{varDecision}}`, `{{varOutcome}}`, `{{playerName}}` |
| `foul`           | `{{playerName}}`                                                     |
| `match_half`     | _(none)_                                                             |
| `penalty`        | _(none)_                                                             |
| `match_end`      | _(none)_                                                             |

## Rugby template variables

| Action type          | Available variables   |
| -------------------- | --------------------- |
| `rugby_match_start`  | `{{teamDescription}}` |
| `rugby_match_end`    | `{{teamDescription}}` |
| `rugby_try`          | `{{playerName}}`      |
| `rugby_conversion`   | `{{playerName}}`      |
| `rugby_penalty_goal` | `{{playerName}}`      |
| `rugby_drop_goal`    | `{{playerName}}`      |
| `rugby_yellow_card`  | `{{playerName}}`      |
| `rugby_red_card`     | `{{playerName}}`      |
| `rugby_match_half`   | _(none)_              |

***

# Football Action Types

Use these action types with `event_category: "sports"` and `event_subcategory: "football"`.

| `action_type`    | Display name   | Supported widget kinds |
| ---------------- | -------------- | ---------------------- |
| `match_start`    | Match Start    | `alert`                |
| `match_half`     | Match Half     | `text-poll`            |
| `match_end`      | Match End      | `text-poll`            |
| `goal`           | Goal           | `emoji-slider`         |
| `shot`           | Shot           | `emoji-slider`         |
| `penalty`        | Penalty        | `text-poll`            |
| `missed_penalty` | Missed Penalty | `text-poll`            |
| `yellow_card`    | Yellow Card    | `text-poll`            |
| `red_card`       | Red Card       | `text-poll`            |
| `substitution`   | Substitution   | `text-poll`            |
| `foul`           | Foul           | `text-poll`            |
| `var_event`      | VAR Event      | `alert`                |

***

# Rugby Action Types

Use these action types with `event_category: "sports"` and `event_subcategory: "rugby"`.

| `action_type`        | Display name | Supported widget kinds |
| -------------------- | ------------ | ---------------------- |
| `rugby_match_start`  | Match Start  | `alert`                |
| `rugby_match_half`   | Match Half   | `text-poll`            |
| `rugby_match_end`    | Match End    | `text-poll`            |
| `rugby_try`          | Try          | `emoji-slider`         |
| `rugby_conversion`   | Conversion   | `emoji-slider`         |
| `rugby_penalty_goal` | Penalty Goal | `emoji-slider`         |
| `rugby_drop_goal`    | Drop Goal    | `emoji-slider`         |
| `rugby_yellow_card`  | Yellow Card  | `text-poll`            |
| `rugby_red_card`     | Red Card     | `text-poll`            |

***

# Response Format

## Success response (single resource)

```json
{
  "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
  "event_id": "srm:match:football-test-001",
  "event_category": "sports",
  "event_subcategory": "football",
  "widget_timeout": "PT15S",
  "status": false,
  "widget_title": "Match Alert",
  "enabled_by": {
    "id": "user-uuid",
    "name": "Jane Producer",
    "image_url": "https://cdn.example.com/avatar.png"
  },
  "match_scheduled_at": "2025-06-15T15:00:00Z",
  "automation_status": "scheduled",
  "automated_actions": [
    {
      "id": "action-uuid",
      "action": "goal",
      "status": "pending",
      "widget_kind": "emoji-slider",
      "publish_delay": "PT0S",
      "max_widgets": null,
      "cooldown_minutes": null,
      "is_active": true,
      "created_at": "2025-06-11T10:00:00Z",
      "updated_at": "2025-06-11T10:00:00Z",
      "widgets": [
        {
          "widget_kind": "emoji-slider",
          "widget_id": "template-uuid",
          "payload": {
            "question": "Rate that goal! 🔥",
            "options": [
              { "image_url": "https://cdn.example.com/fire.png" }
            ]
          }
        }
      ]
    }
  ]
}
```

## `automation_status` values

| Value       | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| `scheduled` | Automation is configured and waiting for the event to start |
| `inflight`  | Automation is processing live events                        |
| `published` | Event has ended and automation is complete                  |

***

# Full Request Examples

## Create — Football automation

```json
{
  "event_id": "srm:match:20250615-mancity-chelsea",
  "event_category": "sports",
  "event_subcategory": "football",
  "program_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "match_scheduled_at": "2025-06-15T15:00:00Z",
  "widget_timeout": "PT20S",
  "automated_actions": [
    {
      "action_type": "goal",
      "enabled": true,
      "widgets": [
        {
          "widget_kind": "emoji-slider",
          "payload": {
            "question": "Rate that goal by {{goalScorer}}! 🔥",
            "options": [
              { "image_url": "https://cdn.example.com/fire.png" },
              { "image_url": "https://cdn.example.com/ok.png" }
            ],
            "localized_data": {
              "fr": { "question": "Notez ce but de {{goalScorer}} ! 🔥" },
              "es": { "question": "¡Valora el gol de {{goalScorer}}! 🔥" }
            }
          }
        }
      ]
    },
    {
      "action_type": "match_start",
      "enabled": true,
      "widgets": [
        {
          "widget_kind": "alert",
          "payload": {
            "text": "🏁 Kick off! {{teamDescription}} are underway!",
            "title": "Match Start",
            "localized_data": {
              "fr": {
                "title": "Début du match",
                "text": "🏁 Coup d'envoi ! {{teamDescription}} sont en route !"
              }
            }
          }
        }
      ]
    },
    {
      "action_type": "yellow_card",
      "enabled": true,
      "publish_delay": "PT3S",
      "widgets": [
        {
          "widget_kind": "text-poll",
          "payload": {
            "question": "Was the {{cardType}} for {{playerName}} deserved?",
            "options": [
              { "description": "Yes, fair call" },
              { "description": "No, too harsh" }
            ],
            "localized_data": {
              "fr": {
                "question": "Le {{cardType}} pour {{playerName}} était-il mérité ?",
                "options": [
                  { "description": "Oui, c'est juste" },
                  { "description": "Non, trop sévère" }
                ]
              }
            }
          }
        }
      ]
    }
  ]
}
```

***

## Create — Rugby automation

```json
{
  "event_id": "opta:match:20250615-saracens-harlequins",
  "event_category": "sports",
  "event_subcategory": "rugby",
  "program_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "match_scheduled_at": "2025-06-15T14:30:00Z",
  "automated_actions": [
    {
      "action_type": "rugby_try",
      "enabled": true,
      "widgets": [
        {
          "widget_kind": "emoji-slider",
          "payload": {
            "question": "What did you think of that try by {{playerName}}?",
            "options": [
              { "image_url": "https://cdn.example.com/amazing.png" },
              { "image_url": "https://cdn.example.com/good.png" }
            ],
            "localized_data": {
              "fr": { "question": "Qu'avez-vous pensé de cet essai de {{playerName}} ?" }
            }
          }
        }
      ]
    },
    {
      "action_type": "rugby_match_start",
      "enabled": true,
      "widgets": [
        {
          "widget_kind": "alert",
          "payload": {
            "text": "🏉 Kick off! {{teamDescription}} get us underway.",
            "title": "Match Start"
          }
        }
      ]
    }
  ]
}
```

***

## Update — Full replace (PUT)

> ⚠️
>
> `PUT` replaces all automated actions. The API deletes actions that exist in the database but are absent from the `PUT` body. The API also deletes and recreates widgets that are not referenced by `widget_id`.

```json
{
  "event_id": "srm:match:20250615-mancity-chelsea",
  "event_category": "sports",
  "event_subcategory": "football",
  "program_id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "match_scheduled_at": "2025-06-15T15:00:00Z",
  "automated_actions": [
    {
      "action_type": "goal",
      "enabled": true,
      "widgets": [
        {
          "widget_kind": "emoji-slider",
          "widget_id": "template-uuid-to-update",
          "payload": {
            "question": "⚽ GOAL! Rate it!",
            "options": [
              { "image_url": "https://cdn.example.com/fire.png" }
            ]
          }
        }
      ]
    }
  ]
}
```

***

# Error Responses

Errors use this shape:

```json
{
  "field_name": ["Error message."]
}
```

For non-field errors, the API returns this shape:

```json
{
  "detail": "Error message."
}
```

## Common validation errors

| Error field         | Cause                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------- |
| `event_category`    | Missing while `event_subcategory` is provided                                           |
| `event_subcategory` | Unknown subcategory for the given `event_category`                                      |
| `partner_type`      | Value is not supported for the given `event_category` / `event_subcategory` combination |
| `event_id`          | Invalid or unrecognised match ID for the partner and programme                          |
| `program_id`        | Programme not found under the authenticated application                                 |
| `automated_actions` | Missing, empty, or contains an invalid action type or widget kind                       |
| `error`             | More than 5 widgets provided for a single action                                        |
| `error`             | Duplicate automation partner already configured for this programme                      |

<br />
