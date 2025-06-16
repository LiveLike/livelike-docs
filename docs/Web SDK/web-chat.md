---
title: Chat
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat | Web SDK | Chat Rooms | LiveLike
  description: >-
    Check out this overview on Web Chat systems of the Engagement SDK to learn
    about chat rooms, chat messages, and more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: web-customizing-empty-chat
      title: Customizing Chats
    - type: basic
      slug: web-chat-room-memberships
      title: Chat Room Memberships
---
## Chat Basics

The `<livelike-chat>` element will insert a fully-functional chat room anywhere on the page it is placed. It is a block-level element by default and will grow vertically to fit its contents.

The `roomid` attribute is required and must be a valid room ID. Chat rooms can be [created through the API](https://docs.livelike.com/v1/reference#create-chat-room).

For versions before 1.20.0 the `programid` attribute is required to load Stickers and Reactions in chat room.

```html
<script>
LiveLike.init({ clientId })
</script>

<livelike-chat roomid="648bb105-bba4-4c3c-8017-e8f390681759"></livelike-chat>
```

## Sizing Chat Elements

A `<livelike-chat>` element is in block display by default and its height property is not set, so the element will grow to contain all messages sent to the room. The height of a chat room can be set with the height CSS property, which will allow the message list to be scrolled and the composer will stay positioned at the bottom of the chat element.

```css
/* Example: create a full-screen chat */
livelike-chat {
  height: 100vh; /* Full height of viewport */
  width: 100vw; /* Full width of viewport */
}
```

## Customizing Chats

Chats can be customized even further, such as by overriding the [empty and loading message list states](doc:web-customizing-empty-chat) or [configuring message timestamps](doc:web-chat-message-timestamps).

## Chat Rooms

### Livelike.createChatRoom

This method creates a new chat room with the ability to pass in two **optional** arguments, `title` and `visibility`. Default visibility for the chatroom is `members`. It returns a Promise that resolves the chat room object.

```javascript
LiveLike.createChatRoom({title: "myTitle", visibility: "everyone"})
	.then(chatroom => console.log(chatroom));
```

### Livelike.getChatRoom

Returns the chatRoom object using the roomId passed in the arguments. It returns a Promise that resolves the chatRoom object containing roomId and title.

```javascript
LiveLike.getChatRoom({roomId: "648bb105-bba4-4c3c-8017-e8f390681759"})
	.then(chatroom => console.log(chatroom));
```

## Get chat user muted status

Using our producer suite website, a producer has the ability to mute a user. Muting a user disables their ability to send messages to the room they were muted in. As an integrator you have the ability to query our backend to find out whether a user is muted or not. This can be achieved using the `getChatUserMutedStatus` function.

```javascript Web
LiveLike.getChatUserMutedStatus({roomId: "<Chat Room ID>"})
  .then(muted_status => console.log(muted_status))
```