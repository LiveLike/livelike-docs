---
title: Custom View in Chat
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom View in Chat | Android SDK | LiveLike
  description: >-
    Android Custom View in Chat is used to show custom view in the LiveLike
    default ChatRoom. Learn more.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Custom View in Chat"
}
[/block]
Custom View in Chat is used to show custom view in the LiveLike default ChatRoom.
This feature allows the integrator to update the UI of each cell of the ChatView.
[block:callout]
{
  "type": "warning",
  "title": "Note:",
  "body": "**This feature does not support reactions and moderation**"
}
[/block]
Currently, we have provided the access to support for custom messages only, which allows the integrator to show any view in the cell for custom messages like widget view, leaderboard, or any other view items.

In order to use this feature, the integrator has to override the ChatViewDelegate in the ChatView class.
[block:callout]
{
  "type": "info",
  "title": "Message:",
  "body": "By providing the value to delegate the LiveLike ChatView support custom message else it will be ignored by the LiveLike ChatView"
}
[/block]
The ChatViewDelegate has two methods to override:

**onCreateViewHolder** 
This method is similar to the method of Recyclerview which provides the parent view and view type and return for RecyclerView.ViewHolder instance.
[block:code]
{
  "codes": [
    {
      "code": "fun onCreateViewHolder*(*parent: ViewGroup, viewType: ChatMessageType*)*: RecyclerView.ViewHolder",
      "language": "kotlin"
    }
  ]
}
[/block]
**onBindViewHolder** 
This method provides the holder instance with livelikeChatMessage data to bind with the view items, also this method provide the chatViewThemeAttribute instance which contains the theme elements related to chat.
Also the ChatView support to show or hide the avatar logo, this method provides the showChatAvatarLogo boolean to provide info related to that.
[block:code]
{
  "codes": [
    {
      "code": " fun onBindViewHolder(\n        holder: RecyclerView.ViewHolder,\n        liveLikeChatMessage: LiveLikeChatMessage,\n        chatViewThemeAttributes: ChatViewThemeAttributes,\n        showChatAvatarLogo: Boolean\n    )",
      "language": "kotlin"
    }
  ]
}
[/block]