---
title: Chat Message Mentions
excerpt: >-
  The Chat Message Mentions feature lets users tag specific profiles in a
  message.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

The Chat Message Mentions feature allows users to tag specific user profiles in chat messages.\
Mentions can be sent along with message creation and will be returned in the response of GET APIs.

## Mention Types

There are two ways to mention users.

* **Explicit mentions**: Doesn’t requiring users to parse the message text manually for mentions.
* **Implicit mention**s: Implicit mentions are automatically extracted from message text by the backend using a specific pattern

> *Currently, we support explicit mentions only. Implicit mentions may be enabled in the future.*

### 1. Explicit Mentions

Client send structured mention data in the POST request when creating a chat message.\
This includes:

* The profile being mentioned (`mentioned_profile_id` or `mentioned_profile_custom_id`)
* The `start_index` and `end_index` : refer to the character positions of the mention placeholder in the message text.

```curl
POST /api/v1/chatroom-messages/
{
  "chat_room_id": "4ec4cdc9-8b80-4ef1-aff2-610125141035",
  "message_event": "message-created",
  "message": "hello @mention1_placeholder, How are you?",
  "mentions": [
    {
      "mentioned_profile_id": "6f273566-8683-4764-b365-3f9b559d70a6",
      // or mentioned_profile_custom_id
      "start_index": 6,
      "end_index": 27
    }
  ]
}
```

At render time, placeholder text in the message can be replaced with the nickname of the mentioned profile.

#### Validation Rules:

1. Max 10 mentions per message
2. Indices must be within message bounds and non-overlapping
3. Provide either `mentioned_profile_id` or `mentioned_profile_custom_id` (not both)
4. `mentioned_profile_custom_id` must resolve to a valid profile
5. Mention is not allowed if:

   * The mentioner has blocked the mentioned profile
   * The mentioned profile has blocked the mentioner

<br />

### Implicit Mentions (Future Scope)

Implicit mentions are automatically extracted from message text by the backend using a specific pattern.\
Example:
`"hello <@profile:1234> and <@profile:5678>"`