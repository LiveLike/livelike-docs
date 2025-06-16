---
title: Deleting chat messages on Web
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Delete Message API"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Minimum Supported SDK Version:",
  "body": "Web: 2.36.0"
}
[/block]
You can use `deleteMessage` API to delete a chat message
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.deleteMessage({ \n  roomId: \"ad56-43hjsf-4214n-gdsk\",\n  messageId: \"dsaf-fdsafkj-dfas132jnc-423\"\n}).then((res) => console.log(res))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Disable delete message"
}
[/block]
You can also disable delete message functionality in stock UI component
[block:code]
{
  "codes": [
    {
      "code": "// query livelike-chat element and remove \"deletemessages\" attribute\nconst livelikeChatNode = document.querySelector('livelike-chat');\nlivelikeChatNode.removeAttribute('deletemessages')",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Remove delete message confirmation"
}
[/block]
You can also disable showing delete message confirmation modal
[block:code]
{
  "codes": [
    {
      "code": "// set confirmActions property of livelike-chat element\nconst livelikeChatNode = document.querySelector('livelike-chat');\n\n// filter out Delete message confirmation type from DEFAULT_CONFIRM_ACTIONS array\nlivelikeChatNode.confirmActions = LiveLike.DEFAULT_CONFIRM_ACTIONS\n.filter(action => action !== LiveLike.ConfirmationType.DELETE_MESSAGE);\n\n// to hide showing confirmation for any actions in future\nlivelikeChatNode.confirmActions = [];",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Custom confirmation renderer"
}
[/block]
You can completely customise how the confirmation modal is rendered. 
[block:code]
{
  "codes": [
    {
      "code": "function customConfirmationRenderer({type, message, onAccept, onReject}){\n // return DOM node\n}\n\nconst livelikeChatNode = document.querySelector('livelike-chat');\nlivelikeChatNode.confirmationRenderer = customConfirmationRenderer",
      "language": "javascript"
    }
  ]
}
[/block]