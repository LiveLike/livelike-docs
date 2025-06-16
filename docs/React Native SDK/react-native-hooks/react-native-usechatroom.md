---
title: useChatRoom
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
      slug: usechatmessages
      title: useChatMessages
---
The purpose of `useChatRoom` hook is to fetch and expose the chatroom resources

##### Example usage

```typescript
const { chatRoom } = useChatRoom({ roomId: "<Room ID>" });
```

## Hook Argument

#### `roomId`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String (**Required**)
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `chatRoom`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [IChatRoomPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IChatRoomPayload)
      </td>

      <td>
        null
      </td>
    </tr>
  </tbody>
</Table>
