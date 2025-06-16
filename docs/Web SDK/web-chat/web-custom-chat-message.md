---
title: Web Custom Chat Message
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Custom Chat Message | Web SDK | LiveLike
  description: >-
    Custom messages allow users to send and receive messages containing any
    data. Learn more about Web Custom Chat Message.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Mininum SDK version",
  "body": "2.11.0"
}
[/block]
Custom messages allow for the sending and receiving of messages containing any data.

When coupled with custom chat UI, this enables the creation of unique chat messages containing videos, embedded apps, widgets, and more.
[block:api-header]
{
  "title": "sendCustomMessage"
}
[/block]
The sendCustomMessage function creates a custom message which is received by other users with the custom-message-created event.

The function takes an object argument with a chat room id string as the roomId property, and a string as the custom_data property. Passing stringified JSON as the custom_data is one way to send various types of data.

**Refer [API Reference](doc:api-reference#api-reference) for more details**
[block:code]
{
  "codes": [
    {
      "code": "const customData = JSON.stringify({\n  title: \"Do you like this feature\",\n  options: [{text: \"Yes\"}, {text: \"No\"}]\n});\n\nLiveLike.sendCustomMessage({\n\troomId: \"6834f1fd-f24d-4538-ba51-63544f9d78eb\",\n  custom_data: customData \n});",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "customMessageRenderer"
}
[/block]
The [`livelike-chat`](doc:web-chat#chat-basics) element contains the property `customMessageRenderer`. This property is a function that returns an HTML element, and has an object parameter containing a `message` object. This function is called whenever a **custom-message-created** event is fired.

The `customMessageRenderer` function allows for the creation of HTML elements when a custom message is received by a user, optionally making use of the `message` object's `custom_data` property.

**Refer [Element reference](doc:api-reference#elements-reference) for prop details**
[block:code]
{
  "codes": [
    {
      "code": "// Define the custom message renderer, access the `message` object, and return an HTML element.\nfunction customMessageRenderer({message}){\n  const customMessage = document.createElement('div');\n  customMessage.className=\"custom-message-renderer\"\n  customMessage.innerText = message.custom_data;\n  return customMessage;\n}\n\n// Set your custom message renderer function as the `customMessageRenderer` property of the `livelike-chat` element.\nconst livelikeChat = document.querySelector('livelike-chat');\nlivelikeChat.customMessageRenderer = customMessageRenderer;",
      "language": "javascript"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Framework specific renderer",
  "body": "Since the `customMessageRenderer` function returns a DOM node, this node could be used as a mounting point to render any framework specific component/view as a child node. For example, rendering React components within the `livelike-chat` Web Component."
}
[/block]