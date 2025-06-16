---
title: User Presence
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
The presence service enables developers to show who is online and who is not. In addition, it provides developers a way to observe and handle when users go online or offline. 

## Presence Concepts

- **Channel** -  a channel is an ambiguous location dependent on your use case. A channel can represent your entire application or smaller areas of your application (ie. a friends list, a chat room, a video, a blog post, etc.) User’s can be present or not present within a channel.
- **Presence Event** - a presence event is an event that is published to observers representing a user joining or leaving a channel.
- **Joining a Channel** - a user joining a channel marks them present in the channel 
- **Leaving a Channel** - a user leaving a channel marks them no longer present in the channel
- **Subscribing to a Channel** - when subscribed to a channel enables a developer to observe Presence Events on the channel
- **Unsubscribing from a Channel** - when unsubscribed from a channel, Presence Events can no longer be observed

> 📘 Demo
> 
> [React.js based demo](https://stackblitz.com/edit/react-ts-bhc5ra?file=LLPresence.tsx) on stack blitz env, fork the env to playground with the demo

## Retrieving a User's Presence

Use `getPresenceUserChannels` API to check which all channels a user is currently present on.

**API Type Definition**: [getPresenceUserChannels](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getPresenceUserChannels)

```javascript
import { getPresenceUserChannels } from "@livelike/javascript"

getPresenceUserChannels({
  userProfileId: "user-id" 
}).then(res => console.log(res))
```

## Retrieving Presence Channel Users

Use `getPresenceChannelUsers` to get list of users present in a channel.

**API Type Definition**: [getPresenceChannelUsers](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getPresenceChannelUsers)

> 🚧 3 second response cache time.
> 
> When retrieving list of users in a given channel, there a response cache time of 3 seconds

```javascript
import { getPresenceChannelUsers } from "@livelike/javascript"

getPresenceChannelUsers({ 
  channel: "test-channel"
}).then(({ channelUsers }) => console.log(channelUsers)) 
```

## Observing Channel's Presence Events

To observe a channel’s presence events, including when a user joins, leaves or has their attributes set, you could use `addPresenceListener` passing a listener callback that gets invoked whenever such events are received.

> 📘 Possible Presence Events
> 
> - **join** - a user has joined a channel and became present
> - **leave** - a user has left a channel and is no longer present
> - **timeout** - a user’s presence in a channel has timed out
> - **updateAttributes** - a user’s presence attributes have changed

**API Type Definition**: [addPresenceListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=addPresenceListener)  
**API Type Definition**: [removePresenceListener](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=removePresenceListener)

```javascript
import { addPresenceListener, removePresenceListener } from "@livelike/javascript"

function onPresenceListener({event, message}){
  // event would be one of the above mentioned presence Event i.e PresenceActionEvent enum
}

// To add a listener callback
addPresenceListener({ channel: "test-channel"}, onPresenceListener)

// to remove a listener callback
removePresenceListener({ channel: "test-channel"}, onPresenceListener)
```

## Set a User’s Presence

To set a User’s Presence in a channel, use the `joinPresenceChannel` API. To remove a User’s Presence in a channel, use the `leavePresenceChannel` API.

**API Type Definition**: [joinPresenceChannel](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=joinPresenceChannel)  
**API Type Definition**: [leavePresenceChannel](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=leavePresenceChannel)

```javascript
import { joinPresenceChannel, leavePresenceChannel } from "@livelike/javascript"

// To join a user presence channel
joinPresenceChannel({ channel: "test-channel"})

// To leave a user presence channel
leavePresenceChannel({ channel: "test-channel"})
```

# Presence Attributes

Presence attributes enable developers to set or get key/pair values associated to a user's presence in a channel. This functionality allows developers to expand on a user's presence even further by providing additional information about the user's presence.  
Some examples of presence attributes are to add location, mood, game score.

> 🚧 About Presence Attributes
> 
> - **The presence attributes data is not persisted anywhere.** When the user disconnects, the presence attributes data is lost. If you require user's presence attributes to be restored on reconnect, be sure to cache that data locally.
> - **Setting presence attributes overwrites any previously set data** for a user on a channel.
> - The user must join a channel before getting or setting attributes.

### Setting User’s Presence Attributes

You can set a user’s Presence attributes by using the `setPresenceUserAttributes` method. Presence attributes is a dictionary of string keys and values and are on a per-channel basis.

**API Type Definition**: [setPresenceUserAttributes](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=setPresenceUserAttributes)

```javascript
import { setPresenceUserAttributes } from "@livelike/javascript"

setPresenceUserAttributes({
   channel: "test-channel",
   attributes: {
     mood: "happy"
   }
})
```

### Getting User’s Presence Attributes

Use `getPresenceUserAttributes` to get a user’s presence attributes in a channel.

**API Type Definition**: [getPresenceUserAttributes](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getPresenceUserAttributes)

```javascript
import { getPresenceUserAttributes } from "@livelike/javascript"

getPresenceUserAttributes({
   channel: "test-channel",
   userProfileId: "test-user-id"
}).then(attributes => console.log(attributes))
```