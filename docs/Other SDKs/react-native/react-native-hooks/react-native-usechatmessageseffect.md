---
title: useChatMessagesEffect
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
      slug: react-native-usemessageitempopover
      title: useMessageItemPopover
---
The purpose of `useChatMessagesEffect` hook is set appropriate message listeners and using callbacks it makes [chat messages resource](https://docs.livelike.com/docs/react-native-usechatmessages) live and reactive

##### Example Usage:

```typescript
useChatMessagesEffect({ roomId: "<Room ID>" });
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
      <td>String</td>
      <td>No Default</td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `removeMessageListener`

<Table align={["left"]}>
  <thead>
    <tr>
      <th>Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Function of type: (arg: [IChatRoomArgs](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IChatRoomArgs), callback: [MessageListenerCallback](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=MessageListenerCallback)) =&gt; Promise&lt;void&gt;</td>
    </tr>
  </tbody>
</Table>