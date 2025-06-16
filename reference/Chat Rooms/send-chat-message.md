---
title: Send a Chat Message
excerpt: ''
api:
  file: engagement-suite.json
  operationId: send-chat-message
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Customizing sender nickname

The `sender_nickname` can be different from the nickname of the profile sending the message, but it requires the profile to have the `change-own-chat-message-sender-nickname` permission. Otherwise the custom sender nickname will be ignored and the profile nickname will be used.
