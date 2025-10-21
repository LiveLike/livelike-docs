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

This API endpoint allows you to assign specific quest variants to user profiles for A/B testing purposes.

## Endpoint

```http
PUT /api/v1/profiles/{profile_id}/quest-variant-assignments/
```

### Base URL
```
https://cf-blast-game-changers.livelikecdn.com
```

## Authentication

This endpoint requires Bearer token authentication.

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Parameters

### Path Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `profile_id` | string | Yes | Unique identifier for the user profile (UUID format) |

### Request Body

The request body should be JSON with the following structure:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `quest_ids` | array[string] | Yes | Array of quest IDs (UUIDs) to assign to the profile |

## Request Example

```bash
curl --location --request PUT 'https://cf-blast-game-changers.livelikecdn.com/api/v1/profiles/ee38a391-abd1-4002-8d76-be4a8a171e3e/quest-variant-assignments/' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
--data '{
    "quest_ids": [
        "e8db7a0d-ffec-4639-ba8d-116b7397dc98"
    ]
}'
```

## Request Body Schema

```json
{
  "type": "object",
  "properties": {
    "quest_ids": {
      "type": "array",
      "items": {
        "type": "string",
        "format": "uuid"
      },
      "description": "Array of quest IDs to assign to the profile"
    }
  },
  "required": ["quest_ids"]
}
```

## Response

### Success Response

**Status:** `200 OK`

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

#### 400 Bad Request
```json
{
  "error": "INVALID_REQUEST",
  "message": "Invalid quest_ids format or missing required fields",
  "details": {
    "invalid_quest_ids": ["invalid-id-format"]
  }
}
```

#### 401 Unauthorized
```json
{
  "error": "UNAUTHORIZED",
  "message": "Invalid or missing authorization token"
}
```

#### 404 Not Found
```json
{
  "error": "PROFILE_NOT_FOUND",
  "message": "Profile with the specified ID was not found"
}
```

#### 422 Unprocessable Entity
```json
{
  "error": "INVALID_QUEST_IDS",
  "message": "One or more quest IDs are invalid or do not exist",
  "details": {
    "invalid_quest_ids": ["non-existent-quest-id"]
  }
}
```

## Usage Notes

- **Profile ID Format**: Must be a valid UUID (e.g., `ee38a391-abd1-4002-8d76-be4a8a171e3e`)
- **Quest IDs Format**: Each quest ID must be a valid UUID
- **Content-Type**: Must be set to `application/json`
- **Authorization**: Bearer token is required for all requests
- **Rate Limiting**: This endpoint may be subject to rate limiting

## Use Cases

This endpoint is typically used for:

- **A/B Testing**: Assigning different quest variants to different user segments
- **Personalization**: Customizing quest experiences based on user profiles
- **Feature Rollouts**: Gradually rolling out new quest features to specific users
- **Experimentation**: Testing different quest configurations with different user groups

## Implementation Example

### JavaScript (Node.js)

```javascript
const assignQuestVariants = async (profileId, questIds, accessToken) => {
  const response = await fetch(`https://cf-blast-game-changers.livelikecdn.com/api/v1/profiles/${profileId}/quest-variant-assignments/`, {
    method: 'PUT',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${accessToken}`
    },
    body: JSON.stringify({
      quest_ids: questIds
    })
  });

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  return await response.json();
};

// Usage
const profileId = 'ee38a391-abd1-4002-8d76-be4a8a171e3e';
const questIds = ['e8db7a0d-ffec-4639-ba8d-116b7397dc98'];
const token = 'YOUR_ACCESS_TOKEN';

assignQuestVariants(profileId, questIds, token)
  .then(result => console.log('Success:', result))
  .catch(error => console.error('Error:', error));
```

### Python

```python
import requests
import json

def assign_quest_variants(profile_id, quest_ids, access_token):
    url = f"https://cf-blast-game-changers.livelikecdn.com/api/v1/profiles/{profile_id}/quest-variant-assignments/"
    
    headers = {
        'Content-Type': 'application/json',
        'Authorization': f'Bearer {access_token}'
    }
    
    data = {
        'quest_ids': quest_ids
    }
    
    response = requests.put(url, headers=headers, json=data)
    response.raise_for_status()
    
    return response.json()

# Usage
profile_id = 'ee38a391-abd1-4002-8d76-be4a8a171e3e'
quest_ids = ['e8db7a0d-ffec-4639-ba8d-116b7397dc98']
token = 'YOUR_ACCESS_TOKEN'

try:
    result = assign_quest_variants(profile_id, quest_ids, token)
    print('Success:', result)
except requests.exceptions.RequestException as e:
    print('Error:', e)
```

## Security Considerations

- Always use HTTPS for API requests
- Store access tokens securely and rotate them regularly
- Validate profile IDs and quest IDs on the client side before making requests
- Implement proper error handling for all response scenarios
- Consider implementing retry logic for transient failures