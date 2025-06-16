---
title: Using chatroom access rules
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
Chatroom access rules are a way to restrict a user from accessing certain features within a chatroom or inside the whole application.

**Directives**: directives are the rules that define the scope for a profile in a chatroom/application\
One such directive is :\
**allow-read**: this directive will only allow read access, denying all the write access to the chatroom

**Use Cases**

**Mute a profile in a Chat**

* To mute a profile in the public chat, create a ChatRoomAccessRule for that Chat Room/Profile pair and set the directive to allow-read.

**Globally mute a profile in a Chat**

* To mute a profile in the public chat, create a ChatRoomAccessRule for that Profile without mentioning the chatroom and set the directive to allow-read.
