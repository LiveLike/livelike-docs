---
title: Listing Application Widgets - Integration Guide
excerpt: >-
  Fetch text-poll and image-poll data across an application, including
  cross-program engagement metrics, pagination, and daily incremental sync
  guidance.
deprecated: false
hidden: false
metadata:
  robots: index
---
## List Widgets For Application

Use `GET /api/v1/applications/<client_id>/widgets/` to retrieve a read-only, cross-program view of poll widget engagement data for a single application. This endpoint is designed for daily incremental loads and returns text poll and image poll widget data with nested option-level vote counts.

```python
import requests

client_id = "YOUR_CLIENT_ID"

r = requests.get(
    f"https://cf-blast.livelikecdn.com/api/v1/applications/{client_id}/widgets/",
    params={
        "kind": ["text-poll", "image-poll"],
        "status": "published",
        "page": 1,
        "page_size": 20,
    },
)

widgets = r.json()
```

<br />

Use the `since` and `until` filters to run incremental syncs based on widget interactions.

### Query Parameters

| Parameter    | Type                   | Required | Default                   | Description                                     |
| ------------ | ---------------------- | -------- | ------------------------- | ----------------------------------------------- |
| `kind`       | `string` (multi-value) | No       | `text-poll`, `image-poll` | Widget types to return                          |
| `status`     | `string`               | No       | `published`               | Widget status filter                            |
| `since`      | `ISO 8601 datetime`    | No       | —                         | Widgets with interactions at or after this time |
| `until`      | `ISO 8601 datetime`    | No       | —                         | Widgets with interactions before this time      |
| `program_id` | `UUID`                 | No       | —                         | Filter by specific program                      |
| `page`       | `integer`              | No       | `1`                       | Page number                                     |
| `page_size`  | `integer`              | No       | `20`                      | Results per page                                |

### Response Fields

#### Widget-level

| Field                                                                                                                                                                | Type       | Description                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------------------- |
| `id`                                                                                                                                                                 | `UUID`     | Widget identifier           |
| `kind`                                                                                                                                                               | `string`   | `text-poll` or `image-poll` |
| `program_id`                                                                                                                                                         | `UUID`     | Program/channel ID          |
| `program_name`                                                                                                                                                       | `string`   | Program/channel name        |
| `client_id`                                                                                                                                                          | `string`   | Application client ID       |
| `question`                                                                                                                                                           | `string`   | Poll question text          |
| `status`                                                                                                                                                             | `string`   | Widget status               |
| `created_at`                                                                                                                                                         | `datetime` | Creation timestamp          |
| `published_at`                                                                                                                                                       | `datetime` | When widget went live       |
| Use this endpoint to fetch all `text-poll` and `image-poll` data across your application for engagement dashboards, analytics reports, and automated data pipelines. |            |                             |

## Endpoint

```http
GET /api/v1/applications/<your_client_id>/widgets/
```

This is a read-only endpoint that returns a unified, cross-program view of widget engagement data for a single application.

## Quick Start

Run the request to fetch all published polls.

```bash
curl "https://api.example.com/api/v1/applications/<your_client_id>/widgets/"
```

## Filtering

### By widget type

```text
# Only text-polls
?kind=text-poll

# Only image-polls
?kind=image-poll

# Both (default if omitted)
?kind=text-poll&kind=image-poll
```

### By status

```text
# Published only (default)
?status=published

# Pending (draft)
?status=pending
```

### By program

```text
?program_id=<program_uuid>
```

### By interaction time

Use `since` and `until` to run incremental syncs based on widget interactions.

```text
# Widgets with votes since a specific time
?since=2026-03-25T00:00:00Z

# Widgets with votes before a specific time
?until=2026-03-28T00:00:00Z

# Widgets with votes in a date range
?since=2026-03-01T00:00:00Z&until=2026-03-15T00:00:00Z
```

### Pagination

```text
# 10 items per page
?page_size=10

# Go to page 2
?page=2&page_size=10
```

### Combined example

```text
?kind=text-poll&status=published&since=2026-03-25T00:00:00Z&program_id=<uuid>&page_size=50
```

## Query Parameters

| Parameter    | Type                   | Required | Default                   | Description                                     |
| ------------ | ---------------------- | -------- | ------------------------- | ----------------------------------------------- |
| `kind`       | `string` (multi-value) | No       | `text-poll`, `image-poll` | Widget types to return                          |
| `status`     | `string`               | No       | `published`               | Widget status filter                            |
| `since`      | `ISO 8601 datetime`    | No       | —                         | Widgets with interactions at or after this time |
| `until`      | `ISO 8601 datetime`    | No       | —                         | Widgets with interactions before this time      |
| `program_id` | `UUID`                 | No       | —                         | Filter by specific program                      |
| `page`       | `integer`              | No       | `1`                       | Page number                                     |
| `page_size`  | `integer`              | No       | `20`                      | Results per page                                |

## Response Structure

```json
{
  "count": 150,
  "next": "https://api.example.com/.../widgets/?page=2",
  "previous": null,
  "results": [
    {
      "id": "3c245bb7-...",
      "kind": "text-poll",
      "program_id": "8d1885c6-...",
      "program_name": "Premier League Matchday",
      "client_id": "your_client_id",
      "question": "Who will win tonight?",
      "status": "published",
      "created_at": "2026-03-20T10:00:00Z",
      "published_at": "2026-03-20T12:00:00Z",
      "interactive_until": "2026-03-20T14:00:00Z",
      "engagement_count": 250,
      "engagement_percent": "0.500",
      "impression_count": 1000,
      "unique_impression_count": 500,
      "custom_data": "backend_ref_123",
      "widget_attributes": [
        {
          "key": "br_id",
          "value": "match_456"
        }
      ],
      "options": [
        {
          "id": "e9a06fb7-...",
          "description": "Team A",
          "vote_count": 150
        },
        {
          "id": "b541ada4-...",
          "description": "Team B",
          "vote_count": 100
        }
      ]
    }
  ]
}
```

## Field Reference

### Widget Fields

| Field                     | Type                | What it tells you                                                              |
| ------------------------- | ------------------- | ------------------------------------------------------------------------------ |
| `id`                      | `UUID`              | Unique widget identifier                                                       |
| `kind`                    | `string`            | `text-poll` or `image-poll`                                                    |
| `program_id`              | `UUID`              | Which program or channel this belongs to                                       |
| `program_name`            | `string`            | Human-readable program name                                                    |
| `question`                | `string`            | The poll question                                                              |
| `status`                  | `string`            | Current state of the widget                                                    |
| `created_at`              | `datetime`          | When it was created                                                            |
| `published_at`            | `datetime`          | When it went live                                                              |
| `interactive_until`       | `datetime` / `null` | When voting closes. `null` means no limit                                      |
| `engagement_count`        | `integer`           | How many users voted                                                           |
| `engagement_percent`      | `string`            | `engagement_count ÷ unique_impression_count`. For example, `"0.500"` means 50% |
| `impression_count`        | `integer`           | Total times the widget was shown                                               |
| `unique_impression_count` | `integer`           | Unique users who saw the widget                                                |
| `custom_data`             | `string` / `null`   | Your custom metadata                                                           |
| `widget_attributes`       | `array`             | Key-value pairs attached to the widget                                         |

### Option Fields

These fields are nested in `options[]`.

| Field         | Type      | What it tells you                       |
| ------------- | --------- | --------------------------------------- |
| `id`          | `UUID`    | Option identifier                       |
| `description` | `string`  | The option text, for example `"Team A"` |
| `vote_count`  | `integer` | How many users picked this option       |
| `image_url`   | `string`  | Option image (`image-poll` only)        |

### Pagination Fields

| Field      | Type           | What it tells you                                              |
| ---------- | -------------- | -------------------------------------------------------------- |
| `count`    | `integer`      | Total matching widgets across all pages                        |
| `next`     | `URL` / `null` | Link to the next page. `null` means this is the last page      |
| `previous` | `URL` / `null` | Link to the previous page. `null` means this is the first page |

## Setting Up Daily Incremental Sync

Follow this flow to keep your analytics data current without reloading the full dataset every day.

### 1. Run the initial full load

Fetch everything the first time.

```http
GET /api/v1/applications/<client_id>/widgets/
```

1. Page through all results by following the `next` link.
2. Store all widget data in your system.
3. Record the current timestamp as your sync marker.

### 2. Run daily incremental loads

Each day, fetch only widgets that had new activity.

```http
GET /api/v1/applications/<client_id>/widgets/?since=<last_sync_timestamp>
```

Recommended flow:

1. Record the current time as `sync_start`.
2. Call the API with `?since=<last_sync_timestamp>`.
3. Page through all results.
4. Update your analytics tables with the new vote counts and engagement data.
5. Save `sync_start` as your new `last_sync_timestamp`.

### What triggers a widget to appear in `since` queries?

User votes. When a user votes on a poll, the widget becomes visible to `since` queries with timestamps before that vote.

### What about widgets with no votes yet?

Widgets with no interaction timestamp do not appear in `since` queries. They do appear in requests without `since`, so your initial full load captures them.

## Comments and Replies

Comment data is available through a separate endpoint. Widgets are linked to comment boards through the widget ID. If you follow the convention of setting `CommentBoard.custom_id` = `widget.uuid`, you can fetch the corresponding comment board using below endpoint, where the comments_count is included in the response.

### Fetch comment counts for a widget

```http
GET /api/v1/comment-boards/?client_id=<client_id>&custom_id=<widget_id>
```

Response:

```json
{
  "comments_count": 45,
  "top_level_comments_count": 30
}
```

| Field                      | What it tells you                     |
| -------------------------- | ------------------------------------- |
| `comments_count`           | Total comments including replies      |
| `top_level_comments_count` | Only root-level comments, not replies |

Reply count = `comments_count - top_level_comments_count` = `15 replies`
