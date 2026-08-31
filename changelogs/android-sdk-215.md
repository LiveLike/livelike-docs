---
title: Android SDK 2.15
author: Shivam Verma
hidden: false
published_at: '2021-04-07T06:11:58.871Z'
---
## Release Notes:

**Android X Support**\
**Added Custom Chat** ([https://docs.livelike.com/docs/chat-session-1](https://docs.livelike.com/docs/chat-session-1))

* Exposed APIs for sending messages and receiving messages and delete messages.
* Loading messages from history
* Remove JoinChatRoom, enterChatRoom, leaveChatRoom and exitChatRoom apis from\
   LiveLikeChatSession, replace the apis with connectToChatRoom apis.
* LiveLikeChatSession now supports only one ChatRoom per session.

**Widget TimeLine** ([https://docs.livelike.com/docs/widget-timeline](https://docs.livelike.com/docs/widget-timeline))

* Widget TimeLine View that lets to display a collection of widgets in a scrollable view
* Widget Became Interactive analytics event
* Chat reaction floating window not disappearing fixed
* More stability and bug fixes