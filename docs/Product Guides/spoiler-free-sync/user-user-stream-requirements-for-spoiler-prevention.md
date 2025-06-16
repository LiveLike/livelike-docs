---
title: Stream Requirements for Preventing Chat Spoilers
excerpt: Stream requirements for preventing users from spoiling each other
deprecated: false
hidden: false
metadata:
  title: Stream Requirements for Preventing Chat Spoilers | LiveLike
  description: >-
    Chat messages sent between users are synchronized to video streams by using
    timecode metadata embedded in video streams.
  robots: index
next:
  description: ''
---
Chat messages sent between users are synchronized to video streams by using timecode metadata embedded in video streams. 

> 🚧 Only HLS support is built-in
>
> The SDKs have built-in plugins for HLS streams with Program Date Time directives supplying timing information. If you use a different stream format, or provide timing information in another way (such as ID3 tags) then you can provide a custom plugin.

## HTTP Live Streaming

When integrating with HLS-based video playback, the SDK's use Program Date Time (PDT) manifest directives to determine time codes for synchronizing chat messages to video playback. For the SDK to be able to synchronize chats to an HLS stream, the stream must contain that metadata, and playback must be allowed on the device.

* EXT-X-PROGRAM-DATE-TIME ([https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5](https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5)) directives at the start of the playlist and after every discontinuity

A reference stream is available here: [https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8](https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8)
