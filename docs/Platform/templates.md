---
title: Templates
excerpt: >-
  Enable producers save reusable content (e.g. a poll question with options, an
  alert's text/image) so they can be reused later when creating a live widget,
  without retyping the same content.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

A template stores metadata like category, subcategory, name, plus a `template_object` which holds the actual content like a particular widget object.

Today `category` only has one valid value: "widgets", but will be extended in future to streaks, quests, leaderboards etc. `subcategory` identifies the specific widget kind (see [Supported widget types](#supported-widget-types)).

## Base URL

```curl
/api/<version>/templates/
```

## Authentication & permissions

Standard application API authentication is required.

- **Read** (`GET`): allowed for any authenticated request.
- **Write** (`POST`, `PUT`, `PATCH`, `DELETE`): requires producer-level permission on the application.

## Endpoints

| Method          | Path               | Description                                                                                                                              |
| --------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `GET`           | `/templates/`      | [List templates](ref:list-templates). Supports filtering (see below). `template_object` is **omitted** from each item in list responses. |
| `POST`          | `/templates/`      | [Create a new template.](ref:create-templates)                                                                                           |
| `GET`           | `/templates/{id}/` | [Retrieve a single template](ref:retrieve-template), including its full `template_object`.                                               |
| `PUT` / `PATCH` | `/templates/{id}/` | [Update a template](ref:update-template)'s `name` and/or `template_object`. `category` and `subcategory` are immutable after creation.   |
| `DELETE`        | `/templates/{id}/` | [Delete the template](ref:delete-template).                                                                                              |

### List filters (query params)

| Param         | Description                                                          |
| ------------- | -------------------------------------------------------------------- |
| `category`    | Filter by category (currently only `widgets`).                       |
| `subcategory` | Filter by widget type, e.g. `text-poll`.                             |
| `is_default`  | Filter to default templates (`true`) or user-created ones (`false`). |

## Request / Response envelope

| Field                       | Type                             | Read/Write | Notes                                                                                     |
| --------------------------- | -------------------------------- | ---------- | ----------------------------------------------------------------------------------------- |
| `id`                        | UUID                             | read-only  |                                                                                           |
| `client_id`                 | string                           | read-only  | Identifies the owning application.                                                        |
| `category`                  | string                           | write-once | Required on create. Only `"widgets"` is currently a valid choice.                         |
| `subcategory`               | string                           | write-once | Required on create. Must be one of the [supported widget types](#supported-widget-types). |
| `name`                      | string                           | read/write | Required. Must be unique within `category`.                                               |
| `is_default`                | boolean                          | read-only  | `true` for built-in default templates.                                                    |
| `using_genie`               | boolean                          | read-only  | `true` if the template was generated using an AI prompt ("Genie").                        |
| `created_on` / `updated_on` | datetime                         | read-only  |                                                                                           |
| `created_by` / `updated_by` | object (`{id, name, image_url}`) | read-only  |                                                                                           |
| `template_object`           | object                           | read/write | Required on create. Shape depends on `subcategory`. Omitted from list responses.          |

### Notes

- Name uniqueness is enforced per `category`, not per `subcategory` — two templates in `widgets` can't share a name even if they're different widget types.
- Creating a template with an unsupported/unknown `subcategory` returns `400` with `"Unsupported subcategory: <value>."`.

## Fields common to every widget type

Every `template_object`, regardless of `subcategory`, accepts/returns these keys in addition to its widget-specific fields:

| Field               | Type                                                | Read/Write | Required                     | Notes                                                                             |
| ------------------- | --------------------------------------------------- | ---------- | ---------------------------- | --------------------------------------------------------------------------------- |
| `localized_data`    | object                                              | read/write | optional (default `{}`)      | Per-locale overrides, keyed by language code, e.g. `{"es": {"question": "..."}}`. |
| `timeout`           | string (ISO-8601 duration)                          | read/write | optional (default `"PT30S"`) | e.g. `"PT30S"` = 30 seconds.                                                      |
| `sponsor_ids`       | array of UUID strings                               | write-only | optional                     | Sponsors to attach.                                                               |
| `sponsors`          | array of objects (`{id, url, logo_url, client_id}`) | read-only  | —                            | Resolved sponsor details, returned in responses.                                  |
| `widget_attributes` | array of `{"key": string, "value": string}`         | read/write | optional                     | Arbitrary key/value metadata attached to the widget.                              |

The per-widget tables below list these alongside each widget's own fields.

***

## Supported widget types

`subcategory` → widget field reference.

### `alert`

| Field               | Type                       | Required  |
| ------------------- | -------------------------- | --------- |
| `title`             | string (≤500 chars)        | optional  |
| `text`              | string (≤500 chars)        | optional  |
| `image_url`         | string (URL, ≤500 chars)   | optional  |
| `link_url`          | string (URL, ≤500 chars)   | optional  |
| `link_label`        | string (≤200 chars)        | optional  |
| `localized_data`    | object                     | optional  |
| `timeout`           | string (ISO-8601 duration) | optional  |
| `sponsor_ids`       | array of UUIDs             | optional  |
| `sponsors`          | array of objects           | read-only |
| `widget_attributes` | array of `{key, value}`    | optional  |

### `video-alert`

| Field               | Type                       | Required     |
| ------------------- | -------------------------- | ------------ |
| `title`             | string (≤200 chars)        | optional     |
| `text`              | string                     | optional     |
| `video_url`         | string (URL, ≤500 chars)   | **required** |
| `link_url`          | string (URL, ≤500 chars)   | optional     |
| `link_label`        | string (≤200 chars)        | optional     |
| `localized_data`    | object                     | optional     |
| `timeout`           | string (ISO-8601 duration) | optional     |
| `sponsor_ids`       | array of UUIDs             | optional     |
| `sponsors`          | array of objects           | read-only    |
| `widget_attributes` | array of `{key, value}`    | optional     |

### `text-ask`

| Field                  | Type                       | Required                                      |
| ---------------------- | -------------------------- | --------------------------------------------- |
| `title`                | string                     | **required**                                  |
| `prompt`               | string                     | **required**                                  |
| `confirmation_message` | string                     | optional (has a default confirmation message) |
| `localized_data`       | object                     | optional                                      |
| `timeout`              | string (ISO-8601 duration) | optional                                      |
| `sponsor_ids`          | array of UUIDs             | optional                                      |
| `sponsors`             | array of objects           | read-only                                     |
| `widget_attributes`    | array of `{key, value}`    | optional                                      |

### `rich-post`

| Field               | Type                       | Required  |
| ------------------- | -------------------------- | --------- |
| `title`             | string (≤200 chars)        | optional  |
| `content`           | string (HTML)              | optional  |
| `localized_data`    | object                     | optional  |
| `timeout`           | string (ISO-8601 duration) | optional  |
| `sponsor_ids`       | array of UUIDs             | optional  |
| `sponsors`          | array of objects           | read-only |
| `widget_attributes` | array of `{key, value}`    | optional  |

### `text-poll`

| Field                      | Type                       | Required     |
| -------------------------- | -------------------------- | ------------ |
| `question`                 | string                     | **required** |
| `options`                  | array of option objects    | optional     |
| `options[].description`    | string                     | **required** |
| `options[].localized_data` | object                     | optional     |
| `localized_data`           | object                     | optional     |
| `timeout`                  | string (ISO-8601 duration) | optional     |
| `sponsor_ids`              | array of UUIDs             | optional     |
| `sponsors`                 | array of objects           | read-only    |
| `widget_attributes`        | array of `{key, value}`    | optional     |

### `image-poll`

| Field                      | Type                       | Required     |
| -------------------------- | -------------------------- | ------------ |
| `question`                 | string                     | **required** |
| `options`                  | array of option objects    | optional     |
| `options[].description`    | string                     | **required** |
| `options[].image_url`      | string (URL, ≤500 chars)   | **required** |
| `options[].localized_data` | object                     | optional     |
| `localized_data`           | object                     | optional     |
| `timeout`                  | string (ISO-8601 duration) | optional     |
| `sponsor_ids`              | array of UUIDs             | optional     |
| `sponsors`                 | array of objects           | read-only    |
| `widget_attributes`        | array of `{key, value}`    | optional     |

### `text-quiz`

| Field                      | Type                                                            | Required                   |
| -------------------------- | --------------------------------------------------------------- | -------------------------- |
| `question`                 | string                                                          | **required**               |
| `choices`                  | array of choice objects (note: key is `choices`, not `options`) | optional                   |
| `choices[].description`    | string                                                          | **required**               |
| `choices[].is_correct`     | boolean                                                         | optional (default `false`) |
| `choices[].localized_data` | object                                                          | optional                   |
| `localized_data`           | object                                                          | optional                   |
| `timeout`                  | string (ISO-8601 duration)                                      | optional                   |
| `sponsor_ids`              | array of UUIDs                                                  | optional                   |
| `sponsors`                 | array of objects                                                | read-only                  |
| `widget_attributes`        | array of `{key, value}`                                         | optional                   |

### `image-quiz`

| Field                      | Type                       | Required                   |
| -------------------------- | -------------------------- | -------------------------- |
| `question`                 | string                     | **required**               |
| `choices`                  | array of choice objects    | optional                   |
| `choices[].description`    | string                     | **required**               |
| `choices[].image_url`      | string (URL, ≤500 chars)   | **required**               |
| `choices[].is_correct`     | boolean                    | optional (default `false`) |
| `choices[].localized_data` | object                     | optional                   |
| `localized_data`           | object                     | optional                   |
| `timeout`                  | string (ISO-8601 duration) | optional                   |
| `sponsor_ids`              | array of UUIDs             | optional                   |
| `sponsors`                 | array of objects           | read-only                  |
| `widget_attributes`        | array of `{key, value}`    | optional                   |

### `text-prediction`

| Field                      | Type                       | Required                                      |
| -------------------------- | -------------------------- | --------------------------------------------- |
| `question`                 | string                     | **required**                                  |
| `confirmation_message`     | string                     | optional (has a default confirmation message) |
| `options`                  | array of option objects    | optional                                      |
| `options[].description`    | string                     | **required**                                  |
| `options[].is_correct`     | boolean                    | optional (default `false`)                    |
| `options[].localized_data` | object                     | optional                                      |
| `localized_data`           | object                     | optional                                      |
| `timeout`                  | string (ISO-8601 duration) | optional                                      |
| `sponsor_ids`              | array of UUIDs             | optional                                      |
| `sponsors`                 | array of objects           | read-only                                     |
| `widget_attributes`        | array of `{key, value}`    | optional                                      |

### `image-prediction`

| Field                      | Type                       | Required                                      |
| -------------------------- | -------------------------- | --------------------------------------------- |
| `question`                 | string                     | **required**                                  |
| `confirmation_message`     | string                     | optional (has a default confirmation message) |
| `options`                  | array of option objects    | optional                                      |
| `options[].description`    | string                     | **required**                                  |
| `options[].image_url`      | string (URL, ≤500 chars)   | **required**                                  |
| `options[].is_correct`     | boolean                    | optional (default `false`)                    |
| `options[].localized_data` | object                     | optional                                      |
| `localized_data`           | object                     | optional                                      |
| `timeout`                  | string (ISO-8601 duration) | optional                                      |
| `sponsor_ids`              | array of UUIDs             | optional                                      |
| `sponsors`                 | array of objects           | read-only                                     |
| `widget_attributes`        | array of `{key, value}`    | optional                                      |

### `image-number-prediction`

| Field                      | Type                       | Required                                      |
| -------------------------- | -------------------------- | --------------------------------------------- |
| `question`                 | string                     | **required**                                  |
| `confirmation_message`     | string                     | optional (has a default confirmation message) |
| `options`                  | array of option objects    | optional                                      |
| `options[].description`    | string                     | **required**                                  |
| `options[].image_url`      | string (URL, ≤500 chars)   | **required**                                  |
| `options[].correct_number` | integer, nullable          | optional                                      |
| `options[].localized_data` | object                     | optional                                      |
| `localized_data`           | object                     | optional                                      |
| `timeout`                  | string (ISO-8601 duration) | optional                                      |
| `sponsor_ids`              | array of UUIDs             | optional                                      |
| `sponsors`                 | array of objects           | read-only                                     |
| `widget_attributes`        | array of `{key, value}`    | optional                                      |

### `cheer-meter`

| Field                      | Type                       | Required     |
| -------------------------- | -------------------------- | ------------ |
| `question`                 | string                     | **required** |
| `options`                  | array of option objects    | optional     |
| `options[].description`    | string                     | **required** |
| `options[].image_url`      | string (URL, ≤500 chars)   | **required** |
| `options[].localized_data` | object                     | optional     |
| `localized_data`           | object                     | optional     |
| `timeout`                  | string (ISO-8601 duration) | optional     |
| `sponsor_ids`              | array of UUIDs             | optional     |
| `sponsors`                 | array of objects           | read-only    |
| `widget_attributes`        | array of `{key, value}`    | optional     |

### `emoji-slider`

| Field                      | Type                       | Required                                                       |
| -------------------------- | -------------------------- | -------------------------------------------------------------- |
| `question`                 | string                     | **required**                                                   |
| `options`                  | array of option objects    | optional                                                       |
| `options[].image_url`      | string (URL, ≤500 chars)   | **required** (no `description` field on this widget's options) |
| `options[].localized_data` | object                     | optional                                                       |
| `localized_data`           | object                     | optional                                                       |
| `timeout`                  | string (ISO-8601 duration) | optional                                                       |
| `sponsor_ids`              | array of UUIDs             | optional                                                       |
| `sponsors`                 | array of objects           | read-only                                                      |
| `widget_attributes`        | array of `{key, value}`    | optional                                                       |

### `social-embed`

| Field               | Type                                   | Required     |
| ------------------- | -------------------------------------- | ------------ |
| `comment`           | string                                 | optional     |
| `items`             | array of item objects (key is `items`) | optional     |
| `items[].url`       | string (URL, ≤500 chars)               | **required** |
| `localized_data`    | object                                 | optional     |
| `timeout`           | string (ISO-8601 duration)             | optional     |
| `sponsor_ids`       | array of UUIDs                         | optional     |
| `sponsors`          | array of objects                       | read-only    |
| `widget_attributes` | array of `{key, value}`                | optional     |

## Related: using a template to create a live widget

Templates are consumed on the individual widget-creation endpoints (e.g. `POST /text-polls/`), not on the template-bank endpoint itself. Widget endpoints that support this accept two extra, write-only fields:

| Field                     | Type    | Notes                                                                                                                                      |
| ------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `using_template_id`       | UUID    | ID of a template. Applies that template's content as defaults; any fields also present in the request body override the template's values. |
| `save_widget_as_template` | boolean | If `true`, saves the widget being created back into the Template Bank as a new template.                                                   |
