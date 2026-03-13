---
title: Update Published Rich Post
excerpt: '`PATCH https://cf-blast.livelikecdn.com/api/v1/rich-posts/{rich_post_id}/`'
deprecated: false
hidden: false
metadata:
  robots: index
---
### Path Params

| Param          | Type            | Description                                                 |
| -------------- | --------------- | ----------------------------------------------------------- |
| `rich_post_id` | `string` (UUID) | required — The unique ID of the published Rich Post to edit |

### Body Params

| Param            | Type     | Description                                                                             |
| ---------------- | -------- | --------------------------------------------------------------------------------------- |
| `title`          | `string` | Updated title of the rich post. Max length 200 characters                               |
| `content`        | `string` | Updated HTML content of the post. Text only — images cannot be changed after publishing |
| `localized_data` | `object` | Localized title and content keyed by locale code                                        |

### Responses

| Code  | Description                                                                                             |
| ----- | ------------------------------------------------------------------------------------------------------- |
| `200` | Rich Post successfully updated. Response includes the updated post object with incremented `edit_count` |
| `400` | Bad request — invalid body params, edit window has expired, or edit limit has been reached              |

> 🚧 **Note:** Editing is only allowed within the configured time window (default: 15 minutes) and up to the configured edit limit (default: 9999). After the window expires or the edit limit is reached, the endpoint will return `400`.
