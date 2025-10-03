---
title: Getting Started with Sceenic (iOS)
excerpt: Get a basic integration up and running with the iOS Sceenic Video Plugin
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This is a developers' guide for setting up a Sceenic Video Plugin configuration for native iOS apps. We will take you through the basic technical steps for configuration and show you how to create video rooms and initiate video calls.

## Prerequisites

* An admin login and registered application on the [Producer Suite](https://cf-blast.livelikecdn.com/) (provided by LiveLike).
* Client ID - Used to initialize the Plugin. See instructions for [retrieving Your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).
* OS: iOS 11+

## Installation

The Plugin can be installed via Cocoapods.

[https://guides.cocoapods.org/using/using-cocoapods.html](https://guides.cocoapods.org/using/using-cocoapods.html)

Add the following to a Podfile:

```swift
target '<application-target-name>' do
    use_frameworks!
    pod 'LiveLikeSceenicVideoPlugin'
end
```

## Initialization

For this step, you will need your Client ID to initialize the Engagement SDK. To get your ClientID, follow the instructions in [Retrieving your Client ID](https://docs.livelike.com/docs/retrieving-important-keys#section-retrieving-client-id).

Import the LiveLikeSceenicVideoPlugin:

```swift
import LiveLikeSceenicVideoPlugin
```

Next, create an instance of the LiveLikeSceenicVideoPlugin.

The Access Token of the User will be stored in User Defaults and may not persist across app installations, devices, and/or platforms. We recommend that you override this default behavior and manage where the User's Access Token is stored.

Use your Client ID to create a LiveLikeSceenicPluginConfig. The LiveLikeSceenicPluginConfig is used to initialize the LiveLikeSceenicVideoPlugin.

```swift
class AppDelegate: UIResponder, UIApplicationDelegate {
  var sceenicPlugin: LiveLikeSceenicVideoPlugin!
  
  func application(_: UIApplication, didFinishLaunchingWithOptions _: [UIApplication.LaunchOptionsKey: Any]?) -> Bool { 
    var config = LiveLikeSceenicPluginConfig(clientID: "<your-client-id>")
    sceenicPlugin = LiveLikeSceenicVideoPlugin(config: config)  
    return true
  }
}
```

## Video rooms

A Video Room is an entity that contains a _Session_ and _Participants_. It is a persistent entity that can be connected to and **interacted** with.

A Video Room Session represents a connection to a Sceenic Video Room. Integrators can interact and modify video calls within a Sceenic Video Room via a Video Room Session.

## Creating a Video Room

To create a Video Room, use the `livelikeSceenicPlugin.createVideoRoom(title: String?, description: String, completion: (Result<VideoRoomResource, Error>) -> Void)` method on your `LiveLikeSceenicVideoPlugin` instance. As a result, you will receive a `VideoRoomResource` which will contain the details of the newly created Video Room or an `Error` object if the creation of a new Video Room fails.

```swift
class SomeClass {
  let plugin: LiveLikeSceenicVideoPlugin
  
  func someMethod(){
    livelikeSceenicPlugin.createVideoRoom(title: "Video Room", description: nil) { result in
    	switch result {
    		case .success(let videoRoomResource):
        	//Handle Success
    		case .failure(let error):
        	//Handle Failure
    	}
		}
  }
}
```

<br />

## Getting Video Room Information

Information on a video room can be retrieved by simply calling the `getVideoRoom(roomID: String, completion: (Result<VideoRoomResource, Error>) -> Void)` function.

```swift
class SomeClass {
  let plugin: LiveLikeSceenicVideoPlugin
  
  func someMethod(){
    livelikeSceenicPlugin.getVideoRoom(roomID: "<video room id>") { result in
    	switch result {
      	case let .success(videoRoomResource):
        	//Handle Success
        case let .failure(error):
        	//Handle Failure
    	}
  	}
  }
```

<br />

## Join a Video Room

The integrator can use `joinVideoRoom(roomID: String, username: String?)` to join an active VideoSession.

The integrator can also use the VideoSession object returned using this API to create a custom UI implementation for the Video Room.

```swift
class SomeClass {
  let plugin: LiveLikeSceenicVideoPlugin
  
  func someMethod(){
    livelikeSceenicPlugin.joinVideoRoom(roomID:"<video room id>", username: "<user name>") { result in
    	switch result {
    		case let .success(videoRoomSession):
        	//Handle Success
    		case let .failure(error):
        	//Handle Failure
    	}
		}
  }
}
```

<br />
