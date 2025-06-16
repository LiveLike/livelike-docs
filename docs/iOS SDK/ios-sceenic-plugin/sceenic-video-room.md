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
[block:api-header]
{
  "title": "Creating a Video Room"
}
[/block]
To create a Video Room, use the `livelikeSceenicPlugin.createVideoRoom(title: String?, description: String, completion: (Result<VideoRoomResource, Error>) -> Void)` method on your `LiveLikeSceenicVideoPlugin` instance. As a result, you will receive a `VideoRoomResource` which will contain the details of the newly created Video Room or an `Error` object if the creation of a new Video Room fails.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let plugin: LiveLikeSceenicVideoPlugin\n  \n  func someMethod(){\n    livelikeSceenicPlugin.createVideoRoom(title: \"Video Room\", description: nil) { result in\n    \tswitch result {\n    \t\tcase .success(let videoRoomResource):\n        \t//Handle Success\n    \t\tcase .failure(let error):\n        \t//Handle Failure\n    \t}\n\t\t}\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting Video Room Information"
}
[/block]
Information on a video room can be retrieved by simply calling the `getVideoRoom(roomID: String, completion: (Result<VideoRoomResource, Error>) -> Void)` function. 
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let plugin: LiveLikeSceenicVideoPlugin\n  \n  func someMethod(){\n    livelikeSceenicPlugin.getVideoRoom(roomID: \"<video room id>\") { result in\n    \tswitch result {\n      \tcase let .success(videoRoomResource):\n        \t//Handle Success\n        case let .failure(error):\n        \t//Handle Failure\n    \t}\n  \t}\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Join a Video Room"
}
[/block]
The integrator can use `joinVideoRoom(roomID: String, username: String?)` to join an active VideoSession. 

The integrator can also use the VideoSession object returned using this API to create a custom UI implementation for the Video Room.
[block:code]
{
  "codes": [
    {
      "code": "class SomeClass {\n  let plugin: LiveLikeSceenicVideoPlugin\n  \n  func someMethod(){\n    livelikeSceenicPlugin.joinVideoRoom(roomID:\"<video room id>\", username: \"<user name>\") { result in\n    \tswitch result {\n    \t\tcase let .success(videoRoomSession):\n        \t//Handle Success\n    \t\tcase let .failure(error):\n        \t//Handle Failure\n    \t}\n\t\t}\n  }\n}",
      "language": "swift"
    }
  ]
}
[/block]