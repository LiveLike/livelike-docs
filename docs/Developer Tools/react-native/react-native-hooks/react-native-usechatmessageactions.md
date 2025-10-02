---
title: useChatMessageActions
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
      slug: usechatmessageseffect
      title: useChatMessagesEffect
---
The purpose of `useChatMessageActions` hook is to abstract out our store actions and exposes actions handlers responsible for updating store value.

##### Example usage

```typescript
const { sendChatMessage, deleteChatMessage } = useChatMessageActions({ 
  roomId: "<Room ID>" 
});
```

## Hook Argument

#### `roomId`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>Type</th>
      <th>Default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>String (**Required**)</td>
      <td>No Default</td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `sendChatMessage`

<Table align={["left"]}>
  <thead>
    <tr>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Function of type: (messageArgs: [ISendMessageArgs](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=ISendMessageArgs)) => Promise&lt;void&gt;</td>
    </tr>
  </tbody>
</Table>

#### `deleteChatMessage`

<Table align={["left"]}>
  <thead>
    <tr>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Function of type: (`{ roomId, chatMessage }`: `{ roomId: any; chatMessage: any; }`) => void</td>
    </tr>
  </tbody>
</Table>