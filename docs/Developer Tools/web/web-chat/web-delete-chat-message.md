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
## Delete Message API

> 📘 Minimum Supported SDK Version:
>
> Web: 2.36.0

You can use `deleteMessage` API to delete a chat message

```javascript
LiveLike.deleteMessage({ 
  roomId: "ad56-43hjsf-4214n-gdsk",
  messageId: "dsaf-fdsafkj-dfas132jnc-423"
}).then((res) => console.log(res))
```

## Disable delete message

You can also disable delete message functionality in stock UI component

```javascript
// query livelike-chat element and remove "deletemessages" attribute
const livelikeChatNode = document.querySelector('livelike-chat');
livelikeChatNode.removeAttribute('deletemessages')
```

## Remove delete message confirmation

You can also disable showing delete message confirmation modal

```javascript
// set confirmActions property of livelike-chat element
const livelikeChatNode = document.querySelector('livelike-chat');

// filter out Delete message confirmation type from DEFAULT_CONFIRM_ACTIONS array
livelikeChatNode.confirmActions = LiveLike.DEFAULT_CONFIRM_ACTIONS
.filter(action => action !== LiveLike.ConfirmationType.DELETE_MESSAGE);

// to hide showing confirmation for any actions in future
livelikeChatNode.confirmActions = [];
```

## Custom confirmation renderer

You can completely customise how the confirmation modal is rendered. 

```javascript
function customConfirmationRenderer({type, message, onAccept, onReject}){
 // return DOM node
}

const livelikeChatNode = document.querySelector('livelike-chat');
livelikeChatNode.confirmationRenderer = customConfirmationRenderer
```
