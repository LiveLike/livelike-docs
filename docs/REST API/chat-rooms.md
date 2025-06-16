---
title: Chat Rooms
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
To create a chat room you will need an Access Token and the Client ID of the application in which the chat room will be created.

Example request:

```
POST /api/v1/chat-rooms/
Authorization: Bearer <access-token>

client_id=<client-id>
```

```
HTTP 201 CREATED
Content-Type: application/json

{
    "id": "b45a3953-3161-4c96-9afd-9f4173d19d4e",
    "url": "https://cf-blast.livelikecdn.com/api/v1/chat-rooms/b45a3953-3161-4c96-9afd-9f4173d19d4e/",
    "client_id": "<client-id>",
    "created_at": "2019-11-05T16:12:56.742590Z",
    "channels": {
        "chat": {
            "sendbird": "chat_b45a3953_3161_4c96_9afd_9f4173d19d4e",
            "pubnub": "chat_b45a3953_3161_4c96_9afd_9f4173d19d4e"
        },
        "control": {
            "pubnub": "control_b45a3953_3161_4c96_9afd_9f4173d19d4e"
        }
    }
}
```