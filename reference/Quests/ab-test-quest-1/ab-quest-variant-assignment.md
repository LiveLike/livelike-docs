---
title: A/B quest variant assignment
api:
  file: profiles.json
  operationId: put_{profile_id}quest-variant-assignments
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
# A/B Quest Variant Assignment

Assign specific quest variants to user profiles for A/B testing purposes.

## Endpoint

```http
PUT /api/v1/profiles/{profile_id}/quest-variant-assignments/
```

**Base URL:** `https://cf-blast.livelikecdn.com`

## Authentication

**Required:** Bearer token authentication

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Parameters

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `profile_id` | string | **Yes** | User profile UUID |

### Headers

| Header | Value | Required | Description |
|--------|-------|----------|-------------|
| `Content-Type` | `application/json` | **Yes** | Request content type |
| `Authorization` | `Bearer {token}` | **Yes** | Bearer authentication token |

### Request Body

**Required Fields:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `quest_ids` | array[string] | **Yes** | Array of quest UUIDs to assign |

**Schema:**
```json
{
  "quest_ids": [
    "e8db7a0d-ffec-4639-ba8d-116b7397dc98"
  ]
}
```

## Complete cURL Example

```bash
curl --location --request PUT 'https://cf-blast.livelikecdn.com/api/v1/profiles/ee38a391-abd1-4002-8d76-be4a8a171e3e/quest-variant-assignments/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--data '{
    "quest_ids": [
        "e8db7a0d-ffec-4639-ba8d-116b7397dc98"
    ]
}'
```

## Response Examples

### Success (200 OK)

```json
{
  "success": true,
  "profile_id": "ee38a391-abd1-4002-8d76-be4a8a171e3e",
  "assigned_quest_ids": [
    "e8db7a0d-ffec-4639-ba8d-116b7397dc98"
  ]
}
```

### Error Responses

| Status | Error Code | Description |
|--------|------------|-------------|
| `400` | `INVALID_REQUEST` | Invalid quest_ids format or missing fields |
| `401` | `UNAUTHORIZED` | Invalid or missing authorization token |
| `404` | `PROFILE_NOT_FOUND` | Profile with specified ID not found |
| `422` | `INVALID_QUEST_IDS` | One or more quest IDs are invalid |

**Error Response Format:**
```json
{
  "error": "ERROR_CODE",
  "message": "Error description",
  "details": {
    "invalid_quest_ids": ["invalid-id"]
  }
}
```

## Request/Response Schema

### Request Schema
```json
{
  "type": "object",
  "properties": {
    "quest_ids": {
      "type": "array",
      "items": {
        "type": "string",
        "format": "uuid"
      }
    }
  },
  "required": ["quest_ids"]
}
```

### Response Schema
```json
{
  "type": "object",
  "properties": {
    "success": {
      "type": "boolean"
    },
    "profile_id": {
      "type": "string",
      "format": "uuid"
    },
    "assigned_quest_ids": {
      "type": "array",
      "items": {
        "type": "string",
        "format": "uuid"
      }
    }
  }
}
```

## Implementation Examples

### JavaScript
```javascript
const response = await fetch(`https://cf-blast.livelikecdn.com/api/v1/profiles/${profileId}/quest-variant-assignments/`, {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': `Bearer ${accessToken}`
  },
  body: JSON.stringify({
    quest_ids: questIds
  })
});
```

### Python
```python
import requests

response = requests.put(
  f"https://cf-blast.livelikecdn.com/api/v1/profiles/{profile_id}/quest-variant-assignments/",
  headers={
    'Content-Type': 'application/json',
    'Authorization': f'Bearer {access_token}'
  },
  json={'quest_ids': quest_ids}
)
```

## Usage Notes

- **Profile ID**: Must be valid UUID format
- **Quest IDs**: Each must be valid UUID format  
- **Rate Limiting**: May apply to this endpoint
- **Use Cases**: A/B testing, personalization, feature rollouts