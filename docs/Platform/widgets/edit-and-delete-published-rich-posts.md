---
title: Edit and Delete Published Rich Posts
excerpt: '  #Guide how to edit and delete end-user published Rich Posts with the REST API.'
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete a Rich Post

A user can permanently delete their own Rich Post at any time. Deleting a post removes it along with all associated engagement data — including replies and reactions — from both the forum and the user's profile. No moderation is required for deletion.

### Request

```
DELETE https://cf-blast.livelikecdn.com/api/v1/rich-posts/{rich_post_id}/
```

| Parameter      | Type            | Description                              |
| -------------- | --------------- | ---------------------------------------- |
| `rich_post_id` | `string` (UUID) | The unique ID of the Rich Post to delete |

### Example

```bash
curl -X DELETE "https://cf-blast.livelikecdn.com/api/v1/rich-posts/{rich_post_id}/" \
  --header "Authorization: Bearer {ACCESS_TOKEN}"
```

### Response

A successful delete returns `204 No Content` with an empty body.

> ❗️ **Authorization is required!**  
> A Rich Post can only be deleted by the user who created it. Always include the user's  Access Token in the `Authorization` header.

***

## Edit a Rich Post

A user can edit the text content of their own Rich Post within a configurable edit limit and time window after posting.

### Rules & Constraints

| Rule                | Default                                                                             |
| ------------------- | ----------------------------------------------------------------------------------- |
| **Text-only edits** | Images cannot be changed after posting                                              |
| **Edit limit**      | 1 edit per post (configurable at application level; default: `9999`)                |
| **Time window**     | Up to 15 minutes after posting (configurable at application level; default: `None`) |

### Rich Post Object — Edit Tracking

Each Rich Post includes an `edit_count` field that tracks the total number of times the post has been updated.

| Field        | Type      | Description                                                                                                |
| ------------ | --------- | ---------------------------------------------------------------------------------------------------------- |
| `edit_count` | `integer` | The number of times the post has been edited. Starts at `0` and increments by `1` on each successful edit. |

This value can be used by your integration to enforce client-side edit limits or display edit history indicators in the UI.

> 📘 **Backward Compatibility**  
> The `Max Edits Allowed` (default: `9999`) and `Time Window` (default: `None`) settings are both configurable at the application level. These defaults ensure backward compatibility for existing integrations. The `edit_count` field is always present on the Rich Post object and reflects the current number of edits made to the post.

### Request

```
PATCH https://cf-blast.livelikecdn.com/api/v1/rich-posts/{rich_post_id}/
```

| Parameter      | Type            | Description                            |
| -------------- | --------------- | -------------------------------------- |
| `rich_post_id` | `string` (UUID) | The unique ID of the Rich Post to edit |

### Request Body

```json
{
  "title": "Updated post title",
  "content": "<p>Updated post content<br></p>",
  "localized_data": {
    "aa": {
      "title": "Localized title",
      "content": "Localized content"
    }
  }
}
```

| Field            | Type            | Required | Description                                                                           |
| ---------------- | --------------- | -------- | ------------------------------------------------------------------------------------- |
| `title`          | `string`        | No       | Updated title of the post                                                             |
| `content`        | `string` (HTML) | No       | Updated HTML content (text only; existing images are preserved but cannot be changed) |
| `localized_data` | `object`        | No       | Localized title and content keyed by locale code                                      |

### Example

```bash
curl -X PATCH "https://cf-blast.livelikecdn.com/api/v1/rich-posts/{rich_post_id}/" \
  --header "Content-Type: application/json" \
  --header "Authorization: Bearer {ACCESS_TOKEN}" \
  --data '{
    "title": "Hello, I updated the title",
    "content": "<p>Updated content here<br></p>",
    "localized_data": {
      "aa": {
        "title": "qwerty",
        "content": "qwerty 2"
      }
    }
  }'
```

### Response

A successful edit returns `200 OK` with the updated Rich Post object, including the incremented `edit_count`.

> ❗️ **Authorization is required!**  
> A Rich Post can only be edited by the user who created it, and only within the allowed time window and edit limit. Always include the user's Access Token in the `Authorization` header.

> 🚧 **Edit window enforcement**  
> Attempts to edit a post outside the allowed time window or after the edit limit has been reached will return an error response. Your integration should handle this gracefully in the UI by hiding the Edit option once the window has passed.
