---
title: Supported Video Players
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Supported Video Players | LiveLike Developer Hub
  description: >-
    If you have a custom player or video production workflow, your developers
    can add custom plugins for common video players. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: spoiler-free-sync
      title: Spoiler Prevention
---
The LiveLike SDKs come bundled with support for common video players. If you have a custom player or video production workflow, your developers can add custom plugins for those situations.
[block:callout]
{
  "type": "info",
  "title": "Video player integration not required",
  "body": "An integration with a video player is only necessary for features like [Spoiler Prevention](doc:spoiler-free-sync). For general usage of features like widgets and chat, integration with the video player is not required."
}
[/block]

[block:api-header]
{
  "title": "Supported Players"
}
[/block]
Support for some players and stream formats are maintained by LiveLike, and are bundled with the SDKs.
[block:parameters]
{
  "data": {
    "h-0": "Player",
    "0-0": "AVPlayer",
    "h-1": "Stream Format",
    "h-2": "Timing",
    "0-1": "HLS",
    "0-2": "Program Date Time",
    "1-0": "ExoPlayer",
    "1-1": "HLS",
    "1-2": "Program Date Time",
    "2-0": "Hls.js",
    "2-1": "HLS",
    "2-2": "Program Date Time",
    "h-3": "Platform",
    "0-3": "iOS",
    "1-3": "Android",
    "2-3": "JavaScript"
  },
  "cols": 4,
  "rows": 3
}
[/block]