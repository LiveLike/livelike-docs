---
title: Sceenic Video Room (iOS)
excerpt: >-
  LiveLike Sceenic Video Plugin allows you to create video rooms. The Plugin
  also provides certain features to manage the video room and its participants.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
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
}
```

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
