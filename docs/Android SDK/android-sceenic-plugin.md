---
title: Sceenic Plugin for Android
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
[block:api-header]
{
  "title": "Getting Started"
}
[/block]
To install the sceenic livelike plugin in android.
Add the below line to your build.gradle of your app module
[block:callout]
{
  "type": "info",
  "body": "implementation 'com.livelike:android-engagement-sdk:livelike-sceenic-plugin:<<android-current-version>>'",
  "title": "Installation"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Sceenic Video SDK",
  "body": "implementation 'com.github.LiveLike:sceenic-video-sdk:1.0.0@aar'"
}
[/block]

[block:api-header]
{
  "title": "VideoRoom"
}
[/block]
VideoRoom contains the basic details related to video calls and contains the identifier which is a token for sceenic communication.
LiveLike has provided API's for create and fetch details of the videoRoom.

## **CreateVideoRoom** 
[block:code]
{
  "codes": [
    {
      "code": "sdk.video().createVideoRoom(<name>,<description>,object :\n                LiveLikeCallback<VideoRoom>() {\n                override fun onResponse(result: VideoRoom?, error: String?) {\n                    result?.let {\n                        //success\n                    }\n                    error?.let {\n                        //error\n                    }\n                }\n\n            })",
      "language": "kotlin"
    }
  ]
}
[/block]
## **VideoRoomDetails** 
[block:code]
{
  "codes": [
    {
      "code": "sdk.video().getVideoRoom(roomId, object : LiveLikeCallback<VideoRoom>() {\n            override fun onResponse(result: VideoRoom?, error: String?) {\n                result?.let {\n                    //success\n                }\n                error?.let {\n                    //error\n                }\n            }\n        })",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "VideoSession"
}
[/block]
VideoSession contains the functionality and exposes API to the integrator related to video calls. 
You can create the videoSession instance from the LiveLike EngagementSDK instance.
[block:code]
{
  "codes": [
    {
      "code": "val videoSession = sdk.createVideoSession()",
      "language": "kotlin"
    }
  ]
}
[/block]
It provides the following features:

### **JoinVideoRoom** 

Once the integrator created the videoRoom, they can connect/join to that video room using joinVideoRoom api.
[block:code]
{
  "codes": [
    {
      "code": "videoSession.joinVideoRoom(<video-room-id>,object : LiveLikeCallback<Unit>() {\n                    override fun onResponse(result: Unit?, error: String?) {\n                        result?.let {\n                            videoSession.setDisplayName(\"Sample Name\")\n                        }\n                    }\n                })",
      "language": "kotlin"
    }
  ]
}
[/block]
### **VideoConnectionState**
We have provided the different states to read the status of the video call connection state.
[block:code]
{
  "codes": [
    {
      "code": "enum class VideoConnectionState {\n    CONNECTING, CONNECTED, DISCONNECTED\n}",
      "language": "kotlin"
    }
  ]
}
[/block]
To listen to these VideoConnectionState , we have expose a stream named **videoConnectionStateEventStream**. 
[block:code]
{
  "codes": [
    {
      "code": "videoSession.videoConnectionStateEventStream.subscribe(this) {\n                when (it) {\n                    VideoConnectionState.CONNECTING -> {\n                        \n                    }\n                    VideoConnectionState.CONNECTED {\n                        \n                    }\n                    VideoConnectionState.DISCONNECTED -> {\n                        \n                    }\n                }\n            }",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Current User Joined the Call** 

Once the user is connected to the video call, in order to listen to the different states of the current user or the states like VideoEnabled or AudioEnabled state for the local user(current user/device). We have provided a stream to which provide you these states of the local participant.
[block:callout]
{
  "type": "warning",
  "title": "Note",
  "body": "For the User term, we are using the Participant object that belongs to Sceenic plugin"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "session.localParticipantEventStream.subscribe(this) { localParticipant -> }\n  ",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Participant**

Participant object belongs to sceenic , it provides the status of audio and video feature, also using the object integrator can enable/disable the audio and video features.
To know about the video state(enable/disable), you can call 
[block:code]
{
  "codes": [
    {
      "code": "participant.isAudioEnabled // To check the audio is enabled or not\nparticipant.disableAudio() // To disable the audio of the local participant for other participants\nparticipant.enableAudio() // To enable the audio of the local participant for other participants\n  \nparticipant.isVideoEnabled // To check the video is enabled or not\nparticipant.disableVideo() // To disable the video of the local participant for other participants\nparticipant.enableVideo() // To enable the video of the local participant for other participants\n  ",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Toggle Video Camera** 
 To Toggle camera for back or front camera
[block:code]
{
  "codes": [
    {
      "code": "videoSession.onSwitchCameraClicked()",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Remote User Joined the Call** 
To listen to the other participants who joined the call or are already on the call. Integrator can call eventStream named **remoteParticipantJoinedEventStream**. It provides the participant object that the integrator can use to show up on the android surface renderer.
[block:code]
{
  "codes": [
    {
      "code": "session.remoteParticipantJoinedEventStream.subscribe(this) { remoteParticipant -> }",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Remote User Left the Call**
To listen to those users who left the video call. The Event Stream provides the id of the participant which the integrator can easily compare with the id of the participant's list to remove from the UI.
[block:code]
{
  "codes": [
    {
      "code": "session.remoteParticipantLeftEventStream.subscribe(this) { participantId -> }",
      "language": "text"
    }
  ]
}
[/block]
### **Leave Current User from the Call** 
In Order to leave the call of the current User.Integrators can call the method below.
[block:code]
{
  "codes": [
    {
      "code": " videoSession.leaveVideoRoom()",
      "language": "kotlin"
    }
  ]
}
[/block]
### **Error Listener Stream**
The error stream allows the integrator to listen to the response to the errors that occur in the video plugin and the service provider.

** VideoRoomErrorType **
The enum VideoRoomErrorType provide the types of error that can occur in the video-plugin which are supposed to be common across various service provider, we have added a type named PLUGIN_ERROR which provides all other error related to the specific service provider 

The Error Listener Stream will provide an instance of VideoRoomErrorDetails data class which contains the above enum type and string provide error details.
[block:api-header]
{
  "title": "LiveLikeSceenicVideoView"
}
[/block]
LiveLike provides the VideoView which allows integrators to use it directly for plugged-in and ready-to-use video calls. The VideoView consists of recyclerView using the adapter from VideoSession it shows the participants in the grid layout, it also automatically adds/removes the participants from the view using the VideoSession.It also consists of the mute/unmute, toggle camera, camera enable/disable, and disconnect the call buttons.
Add the VideoView like any other android view.
[block:code]
{
  "codes": [
    {
      "code": "  <com.livelike.sceenic.plugin.LiveLikeSceenicVideoView\n        android:id=\"@+id/video_view\"\n        android:layout_width=\"match_parent\"\n        android:layout_height=\"match_parent\" />",
      "language": "xml"
    }
  ]
}
[/block]
### **Connect LiveLikeSceenicVideoView to VideoSession** 

To connect the video session to the LiveLikeSceenicVideoView
[block:code]
{
  "codes": [
    {
      "code": "video_view.setSession(videoSession)",
      "language": "kotlin"
    }
  ]
}
[/block]