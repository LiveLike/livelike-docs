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
## Getting Started

To install the sceenic livelike plugin in android.\
Add the below line to your build.gradle of your app module

> 📘 Installation
>
> implementation 'com.livelike:android-engagement-sdk:livelike-sceenic-plugin:{user["android-current-version"]}'

> 📘 Sceenic Video SDK
>
> implementation 'com.github.LiveLike:sceenic-video-sdk:1.0.0\@aar'

## VideoRoom

VideoRoom contains the basic details related to video calls and contains the identifier which is a token for sceenic communication.\
LiveLike has provided API's for create and fetch details of the videoRoom.

## **CreateVideoRoom**

```kotlin
sdk.video().createVideoRoom(<name>,<description>,object :
                LiveLikeCallback<VideoRoom>() {
                override fun onResponse(result: VideoRoom?, error: String?) {
                    result?.let {
                        //success
                    }
                    error?.let {
                        //error
                    }
                }

            })
```

## **VideoRoomDetails**

```kotlin
sdk.video().getVideoRoom(roomId, object : LiveLikeCallback<VideoRoom>() {
            override fun onResponse(result: VideoRoom?, error: String?) {
                result?.let {
                    //success
                }
                error?.let {
                    //error
                }
            }
        })
```

## VideoSession

VideoSession contains the functionality and exposes API to the integrator related to video calls.\
You can create the videoSession instance from the LiveLike EngagementSDK instance.

```kotlin
val videoSession = sdk.createVideoSession()
```

It provides the following features:

### **JoinVideoRoom**

Once the integrator created the videoRoom, they can connect/join to that video room using joinVideoRoom api.

```kotlin
videoSession.joinVideoRoom(<video-room-id>,object : LiveLikeCallback<Unit>() {
                    override fun onResponse(result: Unit?, error: String?) {
                        result?.let {
                            videoSession.setDisplayName("Sample Name")
                        }
                    }
                })
```

### **VideoConnectionState**

We have provided the different states to read the status of the video call connection state.

```kotlin
enum class VideoConnectionState {
    CONNECTING, CONNECTED, DISCONNECTED
}
```

To listen to these VideoConnectionState , we have expose a stream named **videoConnectionStateEventStream**. 

```kotlin
videoSession.videoConnectionStateEventStream.subscribe(this) {
                when (it) {
                    VideoConnectionState.CONNECTING -> {
                        
                    }
                    VideoConnectionState.CONNECTED {
                        
                    }
                    VideoConnectionState.DISCONNECTED -> {
                        
                    }
                }
            }
```

### **Current User Joined the Call**

Once the user is connected to the video call, in order to listen to the different states of the current user or the states like VideoEnabled or AudioEnabled state for the local user(current user/device). We have provided a stream to which provide you these states of the local participant.

> 🚧 Note
>
> For the User term, we are using the Participant object that belongs to Sceenic plugin

```kotlin
session.localParticipantEventStream.subscribe(this) { localParticipant -> }
```

### **Participant**

Participant object belongs to sceenic , it provides the status of audio and video feature, also using the object integrator can enable/disable the audio and video features.\
To know about the video state(enable/disable), you can call 

```kotlin
participant.isAudioEnabled // To check the audio is enabled or not
participant.disableAudio() // To disable the audio of the local participant for other participants
participant.enableAudio() // To enable the audio of the local participant for other participants
  
participant.isVideoEnabled // To check the video is enabled or not
participant.disableVideo() // To disable the video of the local participant for other participants
participant.enableVideo() // To enable the video of the local participant for other participants
```

### **Toggle Video Camera**

 To Toggle camera for back or front camera

```kotlin
videoSession.onSwitchCameraClicked()
```

### **Remote User Joined the Call**

To listen to the other participants who joined the call or are already on the call. Integrator can call eventStream named **remoteParticipantJoinedEventStream**. It provides the participant object that the integrator can use to show up on the android surface renderer.

```kotlin
session.remoteParticipantJoinedEventStream.subscribe(this) { remoteParticipant -> }
```

### **Remote User Left the Call**

To listen to those users who left the video call. The Event Stream provides the id of the participant which the integrator can easily compare with the id of the participant's list to remove from the UI.

```text
session.remoteParticipantLeftEventStream.subscribe(this) { participantId -> }
```

### **Leave Current User from the Call**

In Order to leave the call of the current User.Integrators can call the method below.

```kotlin
videoSession.leaveVideoRoom()
```

### **Error Listener Stream**

The error stream allows the integrator to listen to the response to the errors that occur in the video plugin and the service provider.

**VideoRoomErrorType**\
The enum VideoRoomErrorType provide the types of error that can occur in the video-plugin which are supposed to be common across various service provider, we have added a type named PLUGIN\_ERROR which provides all other error related to the specific service provider 

The Error Listener Stream will provide an instance of VideoRoomErrorDetails data class which contains the above enum type and string provide error details.

## LiveLikeSceenicVideoView

LiveLike provides the VideoView which allows integrators to use it directly for plugged-in and ready-to-use video calls. The VideoView consists of recyclerView using the adapter from VideoSession it shows the participants in the grid layout, it also automatically adds/removes the participants from the view using the VideoSession.It also consists of the mute/unmute, toggle camera, camera enable/disable, and disconnect the call buttons.\
Add the VideoView like any other android view.

```xml
<com.livelike.sceenic.plugin.LiveLikeSceenicVideoView
        android:id="@+id/video_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

### **Connect LiveLikeSceenicVideoView to VideoSession**

To connect the video session to the LiveLikeSceenicVideoView

```kotlin
video_view.setSession(videoSession)
```
