---
title: Toggle Filtered Messages
excerpt: Filtered Messages are the messages having banned words in them
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Every Application has a set banned words configured for themselves. Read more about it here \[https://docs.livelike.com/docs/cms-chat-moderation]

Any message that has banned words present can be filtered out of chat.

## Do not Include Filtered Messages

This is the default setting. Any filtered message will not be shown in chat to receivers.\
Senders still see their original message that they sent in the chat

## Include Filtered Messages

Integrators can choose to show filtered messages to the receivers in the chat (with banned words replaced with asterisks) by using a toggle provided in SDKs\
Senders still see their original message (without asterisks) that they sent in the chat

## Web SDK

**Stock UI**

Integrators can toggle on to show the filtered messages to the receivers using the property showFilteredMessages in component `<livelike-chat>`

```html
<livelike-chat
	showFilteredMessages
	roomid="***"
>
</livelike-chat>
```
```kotlin
val contentSession = engagementSDK.createContentSession(
  "<program-id >",
  includeFilteredChatMessages = true 
)

chat_view.setSession(contentSession.chatSession)
```

**Custom Chat integration**

Integrators can toggle on to see the filtered messages in the API response using the param includeFilteredMessages in method getMessageList

```javascript
LiveLike.getMessageList(roomid, {
  includeFilteredMessages: true,
}).then(list => console.log(list))
```
```kotlin
sdk.createChatSession(
  timecodeGetter ?: this.timecodeGetter,
  errorDelegate,
  includeFilteredChatMessages = true 
)
```