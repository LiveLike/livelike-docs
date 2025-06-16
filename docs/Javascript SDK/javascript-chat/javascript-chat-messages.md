---
title: Chat Messages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-stickers
      title: Stickers
    - type: basic
      slug: javascript-reactions
      title: Reactions
---
[block:api-header]
{
  "title": "Get message list"
}
[/block]
This method is used to get messages of the chat room.

It takes a `roomId` string as an argument and returns a list of messages.
Other optional params:
`count`
`start`
`end`
`includeFilteredMessages` - To include messages with banned words in the response
[block:code]
{
  "codes": [
    {
      "code": "import { getMessageList } from '@livelike/javascript'\n\ngetMessageList(\"<Chat Room ID>\", {\n  includeFilteredMessages: true\n}).then(res => \n  console.log('res', res);\n);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Send message"
}
[/block]
This method is used to send message to a chat room.

It takes an object argument with the required `roomId` string property.
Other arguments are
`message` - For text message
`image_url`, `image_width`, `image_height` - For image message
`sender_image_url` - Optional sender avatar
`custom_data` - Optional custom_data
[block:code]
{
  "codes": [
    {
      "code": "import { sendMessage } from '@livelike/javascript'\n\nconst textMessage = await sendMessage({roomId:'<Chat Room ID>', message:\"Hello\"});\n\nconst imageMessage = await sendMessage({\n  roomId:\"<Chat Room ID>\", \n  image_url:'https://test.com/image.png',\n  image_width: 50,\n  image_height: 150\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Send custom message"
}
[/block]
The sendCustomMessage function creates a custom message which is received by other users with the custom-message-created event.

The function takes an object argument with a chat room id string as the `roomId` property, and a string as the `custom_data` property. Passing stringified JSON as the `custom_data` is one way to send various types of data.

**Refer [API Reference](doc:api-reference#api-reference) for more details**
[block:code]
{
  "codes": [
    {
      "code": "import { sendCustomMessage } from '@livelike/javascript'\n\nconst customData = JSON.stringify({\n  title: \"Do you like this feature\",\n  options: [{text: \"Yes\"}, {text: \"No\"}]\n});\n\nconst customMessage = await sendCustomMessage({\n  roomId: \"6834f1fd-f24d-4538-ba51-63544f9d78eb\",\n  custom_data: customData \n});",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Add message listener"
}
[/block]
This method is used to listen to events that occur within a chat room.
[block:code]
{
  "codes": [
    {
      "code": "import { addMessageListener } from '@livelike/javascript'\n\nconst onMessageCb = (data) => {\n  console.log('data.event', data.event);\n  console.log('data.message', data.message);\n}\n\naddMessageListener({roomId: \"<Chat Room ID>\"}, onMessageCb);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Remove message listener"
}
[/block]
This method is used to remove listeners attached using addMessageListener.
[block:code]
{
  "codes": [
    {
      "code": "import { removeMessageListener } from '@livelike/javascript'\n\nconst onMessageCb = (data) => {\n  console.log('data.event', data.event);\n  console.log('data.message', data.message);\n}\nremoveMessageListener({roomId: \"<Chat Room ID>\"}, onMessageCb);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get message count"
}
[/block]
This method is used to get a number of messages in chat room.

It takes a `roomId` string as an argument and returns a object that contains a roomId as a string and count as a number.
Other optional params:
`since` - DateTime param
`until` - DateTime param
[block:code]
{
  "codes": [
    {
      "code": "import { getMessageCount } from '@livelike/javascript'\n\ngetMessageCount('<Chat Room ID>', {since: \"2020-04-16T16:29:39.158Z\"})\n  .then(r => console.log(r.count))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Delete message"
}
[/block]
This method is used to delete a chat message.
It takes an object argument with the required `roomId` and `messageId`, both string properties.
[block:code]
{
  "codes": [
    {
      "code": "import { deleteMessage } from '@livelike/javascript'\n\ndeleteMessage({ \n  roomId: \"<Chat Room ID>\",\n  messageId: \"<Message ID>\"\n}).then((res) => console.log(res))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Report message"
}
[/block]
Users in chat can report messages, and those reports will show in the Moderation tab for that chat in the Producer Suite. Open the report actions menu, and select Remove to delete the reported message, or Dismiss the report if it is invalid.
The function takes an object argument with a chat room id string as a `roomId` property,
an object argument with a user profile id string as a `profileId` property,
an object argument with a user profile nickname string as a `nickname` property and
an object argument with a message id string as a `messageId` property.
All of them required.
[block:code]
{
  "codes": [
    {
      "code": "import { reportMessage } from '@livelike/javascript'\n\nreportMessage({\n  roomId: \"<Chat Room ID>\",\n  profileId: \"<Profile ID>\",\n  nickname: \"<Nickname>\",\n  messageId: \"<Message ID>\",\n}).then((res) => console.log(res));",
      "language": "javascript"
    }
  ]
}
[/block]