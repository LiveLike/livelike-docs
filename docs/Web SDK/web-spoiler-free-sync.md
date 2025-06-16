---
title: Spoiler Prevention (Web)
excerpt: Preventing spoilers on the web
deprecated: false
hidden: false
metadata:
  title: Spoiler Prevention | Web SDK | LiveLike Developer Hub
  description: >-
    The Web SDK supports spoiler prevention so that widgets and chat messages do
    not appear before the reference action or event.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: spoiler-free-sync
      title: Spoiler Prevention
    - type: basic
      slug: stream-requirements-1
      title: Stream Requirements
---
The Web SDK supports spoiler prevention so that widgets and chat messages do not appear before the action in the video that they are associated with. It does not guarantee that every person will see the same things at the same instant, but it can guarantee that each person will not see chat messages and widgets before seeing the part of the action that those messages and widgets were associated with.
[block:api-header]
{
  "title": "Using Hls.js"
}
[/block]
The Web SDK has a bundled sync strategy for the use of [Hls.js](https://github.com/video-dev/hls.js/) for HLS stream playback on the web.
[block:code]
{
  "codes": [
    {
      "code": "/* Example code for using HlsJsSyncStrategy */\n\nimport { HlsJsSyncStrategy } from '@livelike/engagementsdk\";\nimport Hls from 'hls.js';\n\nconst videoEl = document.getElementById('video');\nconst hls = new Hls({ startPosition: 1 });\nconst syncStrategy = new HlsJsSyncStrategy(hls, videoEl);\nsyncStrategy.hls.loadSource(program.stream_url);\nsyncStrategy.hls.attachMedia(videoEl);\nsyncStrategy.hls.on(Hls.Events.MANIFEST_PARSED, () => {});\nvideoEl.play();\n\nLiveLike.init({ clientId, syncStrategy });",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Using Other Players"
}
[/block]
Other players can be used by implementing a custom Sync Strategy. LiveLike only supports syncing HLS streams because it depends on the [Program Date Time](https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5) metadata from the stream.
[block:callout]
{
  "type": "warning",
  "title": "Other stream requirements",
  "body": "See the [full list of stream requirements](doc:stream-requirements) to ensure sync works user-to-user and producer-to-user."
}
[/block]
The custom sync strategy should extend the `ProgramDateTimeSyncStrategy` class and override the `programDateTime` getter. The getter must return a `Date` instance representing the Program Date Time from the stream. Consult your player's documentation for retrieving that information.
[block:code]
{
  "codes": [
    {
      "code": "/* Example code for creating and using a custom SyncStrategy */\n\nimport { ProgramDateTimeSyncStrategy } from '@livelike/engagementsdk';\n\nexport default class CustomSyncStrategy extends ProgramDateTimeSyncStrategy {\n  constructor(customPlayer) {\n    super(customPlayer);\n    this.customPlayer = customPlayer;\n  }\n\n  get programDateTime() {\n    /* Return a Date instance representing the Program Date Time of the stream */\n    return this.customPlayer.getHlsProgramDateTime();\n  }\n}\n",
      "language": "javascript"
    }
  ]
}
[/block]
Once you have a custom sync strategy, an instance of it can be pass to the SDK initialization step to use it:
[block:code]
{
  "codes": [
    {
      "code": "import CustomSyncStrategy from './custom-sync-strategy';\n\nLiveLike.init({\n  clientId,\n  syncStrategy: new CustomSyncStrategy(customPlayer),\n});",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sending Messages Without Spoilers"
}
[/block]
The built-in chat elements will apply spoiler prevention to each message sent by default. If you want to send messages programmatically without spoilers, use the `LiveLike.sendMessage` method to send a message and include the spoiler timestamp in the `timestamp` parameter.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.sendMessage({\n  message: 'Test message',\n  roomId: 'example-room-id',\n  // The timestamp value can be in the past\n  // It only has to correspond with timecodes in the video stream\n  timestamp: '2020-04-01T00:00:00Z'\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "The `timestamp` argument corresponds to the `program_date_time` in the chat message data payloads."
}
[/block]

[block:api-header]
{
  "title": "ES5 Compatible Custom Sync Strategy"
}
[/block]
If classes aren't available, a plain Object can be created. 

It must include a `currentTimecode` getter, and the getter must return a `Date` instance representing the Program Date Time from the stream. The object can contain any other logic necessary for obtaining the Program Date Time. Consult your player's documentation for retrieving that information.
[block:code]
{
  "codes": [
    {
      "code": "var customSyncStrategy = {\n  get currentTimecode() {\n    /* Return a Date representing the Program Date Time of the stream */\n    return calculateCustomProgramDateTime()\n  }\n}\n\nLiveLike.init({\n  clientId,\n  syncStrategy: customSyncStrategy\n})\n",
      "language": "javascript"
    }
  ]
}
[/block]