---
title: Spoiler Prevention
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Spoiler Prevention | LiveLike Developer Hub | LiveLike
  description: >-
    Sports fans don’t like spoilers, but given the nature of streaming today,
    live viewers never have their videos synchronized. Learn more about spoiler
    prevention.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: spoiler-free-sync
      title: Spoiler Prevention
    - type: basic
      slug: ios-spoiler-free-sync
      title: Spoiler Prevention
    - type: basic
      slug: android-spoiler-free
      title: Spoiler Prevention
    - type: basic
      slug: user-user-stream-requirements-for-spoiler-prevention
      title: User-User Stream Requirements for Spoiler Prevention
    - type: basic
      slug: stream-requirements
      title: Producer-User Stream Requirements for Spoiler Prevention
---
Sports fans don’t like spoilers. Unfortunately given the nature of streaming video today, live viewers are never entirely have their videos synchronized. This is especially exaggerated when using streaming protocols like HLS with large chunk sizes. In such scenarios, user-to-user or producer-to-user communication may result in spoilers that can affect the enjoyment of watching a live game. The LiveLike SDK provides tools to prevent spoilers, so even though not everyone will be watching the same action at the same moment in time, the people watching can be sure they won't be spoiled by someone who is ahead of them in the stream.

## Preventing Chat Spoilers

When users send chat messages to each other, those chat messages are embedded with a timestamp obtained from the video player. A user will only see a message that has been received when they are at the appropriate timestamp in the video.

> 🚧 
> 
> A video player that exposes timing data is required for this functionality. The timing data should come from a common time source between all users, such as from a timestamp embedded in the video stream. Using times information derived from users' device clocks is not suitable.

## Preventing Widgets Spoilers

When a producer sends widgets to users, those widgets are embedded with a timestamp obtained from the video currently playing in the Producer Suite. End-users will only see a widget that has been received when they are at the appropriate timestamp in the video.

> 🚧 
> 
> The program that widgets are being published to inside the Producer Suite needs to be configured with a video stream that matches our Producer-User Stream Requirements for Spoiler Prevention for this scenario to function properly. Users must also be watching on a video player that exposes timing data.

## Basic Requirements

You'll need to provide a video stream that has timecode metadata embedded within it. You'll also need to be using a video player in your experience that can read the timecode metadata from the stream, and developers need to be able to pass the timecode metadata from the player to the LiveLike SDK. The SDK comes with a set of built-in support for common video players and stream formats, see the next section for the full list. If support for your player or stream format isn't bundled, you can still provide your own support by authoring a plugin.

## Integrating Into Your Apps

The LiveLike SDK's come with bundled support for a limited range of video players, but you can add support for your own players and stream formats by providing a custom plugin. Please see the [Supported Video Players](doc:supported-video-players) page for the list of bundled support inside the SDKs. To learn how to integrate spoiler prevention, take a look at the technical documentation for the appropriate platform:

- [iOS SDK](doc:ios-spoiler-free-sync) 
- [Android SDK](doc:android-spoiler-free) 
- [Web SDK](doc:web-spoiler-free-sync)

> 📘 Spoiler prevention is implemented on the client
> 
> All content like chat messages and widgets are delivered live over the network, and spoiler prevention is handled on the client-side so that it can be driven by the user's own local video playback progress. Content that is marked as a spoiler is queued on the device until video playback reaches a point where it is safe to show.

## Testing Your Integration

We host a test HLS stream with program date time metadata, as well as the timestamp burned into the video. It is available here:

- <https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8>

### Testing in Chat

You can test your integration of spoiler prevention for chat by first integrating spoiler prevention with your video player. You can use your own stream for testing, or use [the stream we provide](https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8). Then with two users A and B, follow these steps:

1. Users A and B load the test stream in the integrating app
2. User A pauses playback for a little while so that B can get ahead of them in the stream
3. User B sends a chat message and records the timestamp from the video
4. User A resumes playback and waits until they reach the timestamp recorded by B
5. User A confirms they received the message from B upon reaching the timestamp from earlier, and not before