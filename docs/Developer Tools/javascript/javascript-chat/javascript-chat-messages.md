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
## Get message list

This method is used to get messages of the chat room.

It takes a `roomId` string as an argument and returns a list of messages.\
Other optional params:\
`count`\
`start`\
`end`\
`includeFilteredMessages` - To include messages with banned words in the response

```javascript
import { getMessageList } from '@livelike/javascript'

getMessageList("<Chat Room ID>", {
  includeFilteredMessages: true
}).then(res => 
  console.log('res', res);
);
```

## Send message

This method is used to send message to a chat room.

It takes an object argument with the required `roomId` string property.\
Other arguments are\
`message` - For text message\
`image_url`, `image_width`, `image_height` - For image message\
`sender_image_url` - Optional sender avatar\
`custom_data` - Optional custom\_data

```javascript
import { sendMessage } from '@livelike/javascript'

const textMessage = await sendMessage({roomId:'<Chat Room ID>', message:"Hello"});

const imageMessage = await sendMessage({
  roomId:"<Chat Room ID>", 
  image_url:'https://test.com/image.png',
  image_width: 50,
  image_height: 150
})
```

## Send custom message

The sendCustomMessage function creates a custom message which is received by other users with the custom-message-created event.

The function takes an object argument with a chat room id string as the `roomId` property, and a string as the `custom_data` property. Passing stringified JSON as the `custom_data` is one way to send various types of data.

**Refer[API Reference](doc:api-reference#api-reference) for more details**

```javascript
import { sendCustomMessage } from '@livelike/javascript'

const customData = JSON.stringify({
  title: "Do you like this feature",
  options: [{text: "Yes"}, {text: "No"}]
});

const customMessage = await sendCustomMessage({
  roomId: "6834f1fd-f24d-4538-ba51-63544f9d78eb",
  custom_data: customData 
});
```

## Add message listener

This method is used to listen to events that occur within a chat room.

```javascript
import { addMessageListener } from '@livelike/javascript'

const onMessageCb = (data) => {
  console.log('data.event', data.event);
  console.log('data.message', data.message);
}

addMessageListener({roomId: "<Chat Room ID>"}, onMessageCb);
```

## Remove message listener

This method is used to remove listeners attached using addMessageListener.

```javascript
import { removeMessageListener } from '@livelike/javascript'

const onMessageCb = (data) => {
  console.log('data.event', data.event);
  console.log('data.message', data.message);
}
removeMessageListener({roomId: "<Chat Room ID>"}, onMessageCb);
```

## Get message count

This method is used to get a number of messages in chat room.

It takes a `roomId` string as an argument and returns a object that contains a roomId as a string and count as a number.\
Other optional params:\
`since` - DateTime param\
`until` - DateTime param

```javascript
import { getMessageCount } from '@livelike/javascript'

getMessageCount('<Chat Room ID>', {since: "2020-04-16T16:29:39.158Z"})
  .then(r => console.log(r.count))
```

## Delete message

This method is used to delete a chat message.\
It takes an object argument with the required `roomId` and `messageId`, both string properties.

```javascript
import { deleteMessage } from '@livelike/javascript'

deleteMessage({ 
  roomId: "<Chat Room ID>",
  messageId: "<Message ID>"
}).then((res) => console.log(res))
```

## Report message

Users in chat can report messages, and those reports will show in the Moderation tab for that chat in the Producer Suite. Open the report actions menu, and select Remove to delete the reported message, or Dismiss the report if it is invalid.\
The function takes an object argument with a chat room id string as a `roomId` property,\
an object argument with a user profile id string as a `profileId` property,\
an object argument with a user profile nickname string as a `nickname` property and\
an object argument with a message id string as a `messageId` property.\
All of them required.

```javascript
import { reportMessage } from '@livelike/javascript'

reportMessage({
  roomId: "<Chat Room ID>",
  profileId: "<Profile ID>",
  nickname: "<Nickname>",
  messageId: "<Message ID>",
}).then((res) => console.log(res));
```
