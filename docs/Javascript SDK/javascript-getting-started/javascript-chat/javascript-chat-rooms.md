---
title: Chat Rooms
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
      slug: javascript-chat-memberships
      title: Chat Memberships
---
## Create chat room

This method creates a new chat room with the ability to pass in two optional arguments, title and visibility. The default visibility for the chatroom is members. It returns a Promise that resolves the chat room object.

```javascript JavaScript
import { createChatRoom } from '@livelike/javascript'

const chatroom = await createChatRoom({
  title: "myTitle",
  visibility: "everyone"
})
```

## Create token gated chat room

For creating a token gated chat room you can pass the token\_gates argument in create chat room method along with title and visibiltiy, which will create a token gated chat room. Token gates is an array of object which consist of network\_type and NFT contract address for which token gating is generated or applied. network\_type can be `ethereum`, `chiliz`, `hedera`, `polygon`.

```javascript JavaScript
import { createChatRoom } from '@livelike/javascript'

const chatroom = await createChatRoom({
  title: "myTitle",
  visibility: "everyone",
  token_gates: [{
    contract_address: "0xe60ede23D15Cc5e1807DeC001DA44f9B24d1e458",
      network_type: 'ethereum'
  }]
})
```

## Get chat room

Returns the chatRoom object using the roomId passed in the arguments. It returns a Promise that resolves the chatRoom object containing roomId and title.

## Get available chat rooms

Returns all available chat rooms in an application as a paginated response with results as an array of chat room details.

```javascript JavaScript
import { getChatRooms } from '@livelike/javascript'

const chatrooms = await getChatRooms()
  .then(paginatedResponse => paginatedResponse.results)
```

## Get token gated chat room

For getting token gated chat room details, you can pass roomID and walletAddress as an argument. It will return a Promise that resolves the chatRoom object containing roomId, access, walletDetails.

API Definition: [getTokenGatedChatRoomAccessDetails](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getTokenGatedChatRoomAccessDetails)

```javascript JavaScript
import { getTokenGatedChatRoomAccessDetails } from '@livelike/javascript'

const chatroom = await getTokenGatedChatRoomAccessDetails({
  roomId: "<Chat Room ID>",
  walletAddress:"wallet_address"
});
```

## Get chat user muted status

Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the ability to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus` function.

```javascript
import { getChatUserMutedStatus } from '@livelike/javascript'

getChatUserMutedStatus({roomId: "<Chat Room ID>"})
  .then(muted_status => console.log(muted_status))
```
