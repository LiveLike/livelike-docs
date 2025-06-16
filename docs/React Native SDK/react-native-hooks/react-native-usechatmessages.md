---
title: useChatMessages
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
      slug: react-native-usechatmessageactions
      title: useChatMessageActions
---
The purpose of `useChatMessages` hook is to expose a live reactive chatMessages resource.

##### Example usage

```typescript
const { chatMessages, chatMessagesLoaded } = useChatMessages({
  roomId: "<Room ID>",
});
```

## Hook Argument

#### `roomId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

## Hook Return Value

#### `chatMessages`

| Type                                                                                                                         | Default     |
| :--------------------------------------------------------------------------------------------------------------------------- | :---------- |
| Array of messages of type: [IChatMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatMessage) | Empty Array |

#### `chatMessagesLoaded`

| Type    | Default |
| :------ | :------ |
| boolean | fals    |

> 📘 ℹ️ **Deprecation Notice for Integrators**
>
> We want to inform you that the `useChatMessages` hook is now deprecated and will be removed in a future version of our library. 
>
> **What Does This Mean?**
>
> * Deprecated means that while the `useChatMessages` hook continues to work for now, it's no longer the recommended way to access chat room state and messages.
>
> **Why is it Deprecated?**
>
> * We've introduced the `useChatRoomState` hook, which serves the same purpose but follows a more consistent naming convention for our hooks. This change is part of our efforts to provide better naming conventions for a smoother development experience.
>
> **What Should You Do?**
>
> * If you are currently using the `useChatMessages` hook, we recommend updating your code to use the `useChatRoomState` hook instead. This will ensure that your integration remains compatible with future versions of our library.
> * Please review our updated documentation for examples and guidelines on how to use the `useChatRoomState` hook.
>
> **Timing of Removal:**
>
> * While the `useChatMessages` hook is deprecated, it will continue to work for a limited period. However, to avoid any potential issues in the future, we encourage you to make the transition as soon as possible.
>
> We appreciate your cooperation in this transition and are here to assist you with any questions or concerns you may have.
