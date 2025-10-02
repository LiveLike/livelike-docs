---
title: useChatMessageMenuItemActions
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
The `useChatMessageMenuItemActions` hook is designed to handle moderation menu item actions in a chat application. It provides functions that are executed when a user clicks on moderation menu items associated with chat messages.

##### Example usage

```typescript
const { deleteMessageApiFn, reportMessageApiFn, blockUserApiFn } = useChatMessageMenuItemActions({ 
  messageDetails: {} 
});
```

## Hook Argument

#### `messageDetails`

| Type                                                                                                                                                     | Default    |
| :------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------- |
| [UseChatMessageMenuItemActionsArg](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=UseChatMessageMenuItemActionsArg) (**Required**) | No Default |

## Hook Return Value

#### `deleteMessageApiFn`

A function executed when the user clicks the `Delete` menu item. This can be used to delete the user's own message.

| Type                         |
| :--------------------------- |
| Function of type: () => void |

#### `reportMessageApiFn`

A function executed when the user clicks the `Report` menu item. This can be used to report someone else's message.

| Type                         |
| :--------------------------- |
| Function of type: () => void |

#### `blockUserApiFn`

A function executed when the user clicks the `Block` menu item. This can be used to block the user associated with the message.

| Type                         |
| :--------------------------- |
| Function of type: () => void |
