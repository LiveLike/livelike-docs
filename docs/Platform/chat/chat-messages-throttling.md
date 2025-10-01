---
title: Chat Messages Throttling
excerpt: >-
  Integrators can configure throttling to control how frequently fans are
  allowed to send chat messages in a room. This helps reduce spam and maintain
  healthy conversation flow without completely disabling chat activity.
deprecated: false
hidden: false
metadata:
  robots: index
---
For example, if throttling is set to 30 seconds, a user can only send one message every 30 seconds per room. Throttling can be set only in seconds. Values 0 seconds disabling throttle.

**Use Cases:**
•	**Spam Prevention:** Prevent a single fan from flooding a chat with rapid messages.
•	**Room-Specific Throttling:** Apply different throttle policies per room depending on audience size or event type.
•	**Fair Participation:** Ensure all fans have a chance to contribute to the discussion.

How to set chat messages throttling (there are 3 ways to do it):

1. **From admin panel in the cms**:

![](https://files.readme.io/8b9d51cdcefc29b3de586692e71b96e189e0a6a59ac2b2bda0b8b5795da3617c-Screenshot_2025-09-11_at_12.51.33.png)

2. **From CMS during creation or update of chatroom**:

**Create:**

![](https://files.readme.io/afe24456b3ca614fb4db090bc972f8a426ced3e5ebb1fd7e8b15857935ef7723-Screenshot_2025-09-11_at_13.04.28.png)

<br />

**Edit:**

![](https://files.readme.io/3c84a032cedd61fc3679f4be74e75b68bf323c1a9b2f71a7ac6510716bcce770-Screenshot_2025-09-11_at_12.53.05.png)

3. **From API:**

 **POST:** [https://cf-blast.livelikecdn.com/api/v1/chat-rooms](https://cf-blast.livelikecdn.com/api/v1/chat-rooms)

 **PATCH** [https://cf-blast.livelikecdn.com/api/v1/chat-rooms/:id](https://cf-blast.livelikecdn.com/api/v1/chat-rooms/)

  Parameter in the body of request **chat_message_throttle_seconds**: number
