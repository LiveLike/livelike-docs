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

* **Channel** -  a channel is an ambiguous location dependent on your use case. A channel can represent your entire application or smaller areas of your application (ie. a friends list, a chat room, a video, a blog post, etc.) User’s can be present or not present within a channel.
* **Presence Event** - a presence event is an event that is published to observers representing a user joining or leaving a channel.
* **Joining a Channel** - a user joining a channel marks them present in the channel 
* **Leaving a Channel** - a user leaving a channel marks them no longer present in the channel
* **Subscribing to a Channel** - when subscribed to a channel enables a developer to observe Presence Events on the channel
* **Unsubscribing from a Channel** - when unsubscribed from a channel, Presence Events can no longer be observed

## Retrieving a User's Presence

To check which all channels a user is currently present on.

```swift
import LiveLikeSwift

class SomeClass {
  let livelike: LiveLike
  
  func someMethod() {
        livelike.presenceClient.whereNow(
            for: "<profile-id>"
        ) { result in
            switch result {
            case .success(let channels):
                // handle success
            case .failure(let error):
                // handle failure
            }
        }
   }
}
```
```kotlin
val presenceClient = liveLikeSdk.presenceClient()

presenceClient.whereNow(
    <profile-id>,
    object : LiveLikeCallback<List<String>>() {
        override fun onResponse(result: List<String>?, error: String?) {
            error?.let{
                // handle failure
            }
            result?.let {
                // handle success
            }
        }
    }
)
```
```javascript Web
LiveLike.getPresenceUserChannels({ 
  userProfileId: "<profile-id>" 
}).then(res => console.log(res))
```

## Retrieving Presence Channel Users

To get list of users present in a channel.

> 🚧 3 second response cache time.
>
> When retrieving list of users in a given channel, there a response cache time of 3 seconds

```javascript Web
LiveLike.getPresenceChannelUsers({ 
  channel: "<channel-1>"
}).then(({channelUsers}) => console.log(channelUsers)) 
```

## Observing Channel's Presence Events

To observe a channel’s presence events, including when a user joins, leaves or has their attributes set.\
In case of Mobile SDK's, you should `subscribe` to a presence channel. To stop observing a channel’s presence events use `unsubscribe`.

> 📘 Possible Presence Events
>
> * **join** - a user has joined a channel and became present
> * **leave** - a user has left a channel and is no longer present
> * **timeout** - a user’s presence in a channel has timed out
> * **updateAttributes** - a user’s presence attributes have changed

```swift
import LiveLikeSwift

class SomeClass {
   let livelike: LiveLike
  
   func someMethod() {
     livelike.presenceClient.setDelegate(self)
     
     // to subscribe
     livelike.presenceClient.subscribe(to: ["<channel-1>", "<channel-2>"])
     // to unsubscribe   
     livelike.presenceClient.unsubscribe(to: ["<channel-1>", "<channel-2>"])
   }
}

extension SomeClass: PresenceClientDelegate {
    func presenceClient(
        _ presenceClient: PresenceClient,
        didReceivePresenceEvents presenceEvents: [PresenceEvent]
    ) {
        presenceEvents.forEach { presenceEvent in
            switch presenceEvent.action {
            case .join:
                // handle a join event
            case .leave:
                // handle a leave event
            case .timeout:
                // handle a timeout event
            case .updateAttributes:
                // handle an updateAttributes event
            }
        }   
    }
}
```
```kotlin
val presenceClient = liveLikeSdk.presenceClient()

val subscription = presenceClient.subscribeForPresence(
    setOf("<channel-1>", "<channel-2>"),
) { presenceEvent ->
    when (presenceEvent) {
        is JoinEvent -> {
            // handle a join event
        }
        is LeaveEvent -> {
            // handle a leave event
        }
        is TimeoutEvent -> {
            // handle a timeout event
        }
        is UpdateEvent -> {
            // handle an updateAttributes event
        }
    }
}

presenceClient.unsubscribeForPresence(subscription)
```
```javascript Web
function onPresenceListener({event, message}){
  // event would be one of the above mentioned presence Event i.e LiveLike.PresenceEventAction enum
}

// To add a listener callback
LiveLike.addPresenceListener({ channel: "<channel-1>" }, onPresenceListener)

// to remove a listener callback
LiveLike.removePresenceListener({ channel: "<channel-1>" }, onPresenceListener)
```

## Set a User’s Presence

To set a User’s Presence in a channel, use the `join` method. To remove a User’s Presence in a channel, use the `leave` method.

```swift
import LiveLikeSwift

class SomeClass {
   let livelike: LiveLike
   
   func someMethod() {
     
     // join channel
     livelike.presenceClient.join(["<channel-1>", "<channel-2>"])
     
     // leave channel
     livelike.presenceClient.leave(["<channel-1>", "<channel-2>"])
   }
}
```
```kotlin
val presenceClient = liveLikeSdk.presenceClient()

presenceClient.joinChannels(
    setOf("<channel-1>", "<channel-2>"),
)

presenceClient.leaveChannels(
  setOf("<channel-1>", "<channel-2>")
)
```
```javascript Web
// To join a user presence channel
LiveLike.joinPresenceChannel({ channel: "<channel-1>" })

// To leave a user presence channel
LiveLike.leavePresenceChannel({ channel: "<channel-1>" })
```

# Presence Attributes

Presence attributes enable developers to set or get key/pair values associated to a user's presence in a channel. This functionality allows developers to expand on a user's presence even further by providing additional information about the user's presence.\
Some examples of presence attributes are to add location, mood, game score.

> 🚧 About Presence Attributes
>
> * **The presence attributes data is not persisted anywhere**. When the user disconnects, the presence attributes data is lost. If you require user's presence attributes to be restored on reconnect, be sure to cache that data locally.
> * **Setting presence attributes overwrites any previously set data** for a user on a channel.
> * The user must join a channel before getting or setting attributes.

### Setting User’s Presence Attributes

You can set a user’s Presence Attributes by using the `setAttributes` method. Presence attributes is a dictionary of string keys and values and are on a per-channel basis.

```swift
import LiveLikeSwift

class SomeClass {
   let livelike: LiveLike
   
   func someMethod() {
        let attributes: PresenceClientAttributes = [
            "real-world-location" : "usa",
            "team" : "blue"
        ]
        
        livelike.presenceClient.setAttributes(
            for: ["<channel-1>", "<channel-2>"],
            with: attributes
        ) { result in
            switch result {
            case .failure(let error):
                // handle error
            case .success(let attributes):
                // handle success
        }
   }
}
```
```kotlin
val presenceClient = liveLikeSdk.presenceClient()

presenceClient.setAttributes(
    setOf("<channel-1>", "<channel-2>"),
    mapOf(
        "real-world-location" to "usa",
        "team" to "blue"
    )
)
```
```javascript Web
LiveLike.setPresenceUserAttributes({
   channel: "<channel-1>",
   attributes: {
     "real-world-location" : "usa",
     "team" : "blue"
   }
})
```

### Getting User’s Presence Attributes

To get a user’s presence attributes in a channel, use the `getAttributes` method.

```swift
import LiveLikeSwift

class SomeClass {
   let livelike: LiveLike
   
   func someMethod() {
        livelike.presenceClient.getAttributes(
            for: "<profile-id>"
            on: ["<channel-1>", "<channel-2>"]
        ) { result in
            switch result {
            case .failure(let error):
                // handle error
            case .success(let attributes):
                // handle success
        }
   }
}
```
```kotlin
val presenceClient = liveLikeSdk.presenceClient()

presenceClient.getAttributes(
    "<profile-id>",
    setOf("<channel-1>", "<channel-2>"),
    object : LiveLikeCallback<Map<String, Map<String, String>>>() {
        override fun onResponse(
            result: Map<String, Map<String, String>>?,
            error: String?
        ) {
            error?.let {
                // handle error
            }
            result?.let{
                // handle success
            }
        }
    }
)
```
```javascript Web
LiveLike.getPresenceUserAttributes({
   channel: "<channel-1>",
   userProfileId: "<profile-id>"
}).then(attributes => console.log(attributes))
```
