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
Every Application has a set banned words configured for themselves. Read more about it here [https://docs.livelike.com/docs/cms-chat-moderation]

Any message that has banned words present can be filtered out of chat.
[block:api-header]
{
  "title": "Do not Include Filtered Messages"
}
[/block]
This is the default setting. Any filtered message will not be shown in chat to receivers.
Senders still see their original message that they sent in the chat
[block:api-header]
{
  "title": "Include Filtered Messages"
}
[/block]
Integrators can choose to show filtered messages to the receivers in the chat (with banned words replaced with asterisks) by using a toggle provided in SDKs
Senders still see their original message (without asterisks) that they sent in the chat
[block:api-header]
{
  "title": "Web SDK"
}
[/block]
**Stock UI**

Integrators can toggle on to show the filtered messages to the receivers using the property showFilteredMessages in component <livelike-chat>
[block:code]
{
  "codes": [
    {
      "code": "<livelike-chat\n\tshowFilteredMessages\n\troomid=\"***\"\n>\n</livelike-chat>",
      "language": "html"
    },
    {
      "code": "val contentSession = engagementSDK.createContentSession(\n  \"<program-id >\",\n  includeFilteredChatMessages = true \n)\n\nchat_view.setSession(contentSession.chatSession)",
      "language": "kotlin"
    }
  ]
}
[/block]
**Custom Chat integration**

Integrators can toggle on to see the filtered messages in the API response using the param includeFilteredMessages in method getMessageList
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getMessageList(roomid, {\n  includeFilteredMessages: true,\n}).then(list => console.log(list))",
      "language": "javascript"
    },
    {
      "code": "sdk.createChatSession(\n  timecodeGetter ?: this.timecodeGetter,\n  errorDelegate,\n  includeFilteredChatMessages = true \n)",
      "language": "kotlin",
      "name": null
    }
  ]
}
[/block]