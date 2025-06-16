---
title: Chat Methods
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat API Methods | Web SDK | LiveLike
  description: >-
    The LiveLike Web SDK contains various chat methods which can be used to
    build chats. Learn more about Web Chat Messages.
  robots: index
next:
  description: ''
---
The Web SDK contains various chat methods which can be used to build chats.
[block:api-header]
{
  "title": "getMessageList"
}
[/block]
This method is used to get messages of the chat room.

It takes a **roomId** string as an argument and returns a list of messages.

Other optional params:
**count**
**start**
**end**
**includeFilteredMessages** - To include messages with banned words in the response
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getMessageList(\"*****\", {\n  includeFilteredMessages: true\n}).then(res => \n  console.log('res', res);\n);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "sendMessage"
}
[/block]
This method is used to send message to a chat room. 

It takes an object argument with the required ** roomId** string property. 
Other arguments are
For text message - ** message**
For image message - ** image_url**, ** image_width**, ** image_height**
Optional sender avatar - ** sender_image_url**
Optional custom_data - ** custom_data**
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.sendMessage({roomId:'*****', message:\"Hello\"});\n\nLiveLike.sendMessage({\n  roomId:\"*****\", \n  image_url:'https://test.com/image.png',\n  image_width: 50,\n  image_height: 150\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "addMessageListener"
}
[/block]
This method is used to listen to events that occur within a chat room. 
[block:code]
{
  "codes": [
    {
      "code": "const callback = (data) => {\n  console.log('data.event', data.event);\n  console.log('data.message', data.message);\n}\n\nLiveLike.addMessageListener({roomId: \"*****\"}, callback);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "removeMessageListener"
}
[/block]
This method is used to remove listeners attached using addMessageListener.
[block:code]
{
  "codes": [
    {
      "code": "const callback = (data) => {\n  console.log('data.event', data.event);\n  console.log('data.message', data.message);\n}\n\nLiveLike.removeMessageListener({roomId: \"*****\"}, callback);",
      "language": "javascript"
    }
  ]
}
[/block]