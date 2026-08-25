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

| Method          | Path               | Description                                                                                                        |
| --------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------ |
| `GET`           | `/templates/`      | List templates. Supports filtering (see below). `template_object` is **omitted** from each item in list responses. |
| `POST`          | `/templates/`      | Create a new template.                                                                                             |
| `GET`           | `/templates/{id}/` | Retrieve a single template, including its full `template_object`.                                                  |
| `PUT` / `PATCH` | `/templates/{id}/` | Update a template's `name` and/or `template_object`. `category` and `subcategory` are immutable after creation.    |
| `DELETE`        | `/templates/{id}/` | Delete the template.                                                                                               |

### List filters (query params)

| Param         | Description                                                          |
| ------------- | -------------------------------------------------------------------- |
| `category`    | Filter by category (currently only `widgets`).                       |
| `subcategory` | Filter by widget type, e.g. `text-poll`.                             |
| `is_default`  | Filter to default templates (`true`) or user-created ones (`false`). |

## Response envelope

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
