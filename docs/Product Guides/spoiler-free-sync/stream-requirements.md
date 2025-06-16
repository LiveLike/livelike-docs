---
title: Stream Requirements for Preventing CMS Spoilers
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Stream Requirements for Preventing CMS Spoilers | LiveLike
  description: >-
    Pop-ups and chat messages sent from the Producer Site are synchronized to
    video streams by using timecode metadata embedded in video streams.
  robots: index
next:
  description: ''
---
Pop-ups and chat messages sent from the Producer Site are synchronized to video streams by using timecode metadata embedded in video streams. Note that the following requirements only apply to the Producer Site and are not needed for User-User Chat Spoiler Prevention.

> 🚧 Only HLS support is built-in
>
> The SDKs have built-in plugins for HLS streams with Program Date Time directives supplying timing information. If you use a different stream format, or provide timing information in another way (such as ID3 tags) then you can provide a custom plugin.

## General Requirements

* Video preview must be enabled in the Producer Suite
* If the producer and the audience are watching two different streams, those streams should have matching metadata

## HTTP Live Streaming

When integrating with HLS-based video playback, the SDK's use Program Date Time (PDT) manifest directives to determine time codes for syncing widgets and chat messages to video playback. For producers to be able to synchronize widgets to an HLS stream, the stream must contain that metadata, and playback must be allowed within the Producer Suite. That means that playback of the stream cannot be restricted on the web from the producer by user agent, IP address, geolocation, etc. The technical requirements are listed here:

* EXT-X-PROGRAM-DATE-TIME ([https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5](https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5)) directives at the start of the playlist and after every discontinuity
* Cross-Origin Resource Sharing ([https://www.w3.org/TR/cors/](https://www.w3.org/TR/cors/)) (CORS) enabled on playlist and segment files
* Stream allows access from supported browser User Agents
* Manifest and segment files do not require a `Referer` header in HTTP requests
* Stream is not geo-blocked from where producers are accessing the Producer Suite from
* Stream allows access from IP addresses that producers are accessing Producer Suite from

A reference stream is available here: [https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8](https://cf-streams.livelikecdn.com/live/colorbars/index.m3u8)

If the PDT metadata is not available then there is no time code for publishing tools to reference for synchronization. If CORS is not enabled then playback in the Producer Suite will typically not work due to browser security restrictions. Some browsers allow for content security policies like CORS to be toggled enabled/disabled, but toggling that can be an onerous process for non-technical users depending on the browser.
