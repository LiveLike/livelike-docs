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

## getMessageList

This method is used to get messages of the chat room.

It takes a **roomId** string as an argument and returns a list of messages.

Other optional params:\
**count**\
**start**\
**end**\
**includeFilteredMessages** - To include messages with banned words in the response

```javascript
LiveLike.getMessageList("*****", {
  includeFilteredMessages: true
}).then(res => 
  console.log('res', res);
);
```

## sendMessage

This method is used to send message to a chat room. 

It takes an object argument with the required **roomId** string property.\
Other arguments are\
For text message - **message**\
For image message - **image\_url** , **image\_width** , **image\_height**\
Optional sender avatar - **sender\_image\_url**\
Optional custom\_data - **custom\_data**

```javascript
LiveLike.sendMessage({roomId:'*****', message:"Hello"});

LiveLike.sendMessage({
  roomId:"*****", 
  image_url:'https://test.com/image.png',
  image_width: 50,
  image_height: 150
})
```

## addMessageListener

This method is used to listen to events that occur within a chat room. 

```javascript
const callback = (data) => {
  console.log('data.event', data.event);
  console.log('data.message', data.message);
}

LiveLike.addMessageListener({roomId: "*****"}, callback);
```

## removeMessageListener

This method is used to remove listeners attached using addMessageListener.

```javascript
const callback = (data) => {
  console.log('data.event', data.event);
  console.log('data.message', data.message);
}

LiveLike.removeMessageListener({roomId: "*****"}, callback);
```
