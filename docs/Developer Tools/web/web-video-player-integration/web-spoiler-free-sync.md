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

## Using Hls.js

The Web SDK has a bundled sync strategy for the use of [Hls.js](https://github.com/video-dev/hls.js/) for HLS stream playback on the web.

```javascript
/* Example code for using HlsJsSyncStrategy */

import { HlsJsSyncStrategy } from '@livelike/engagementsdk";
import Hls from 'hls.js';

const videoEl = document.getElementById('video');
const hls = new Hls({ startPosition: 1 });
const syncStrategy = new HlsJsSyncStrategy(hls, videoEl);
syncStrategy.hls.loadSource(program.stream_url);
syncStrategy.hls.attachMedia(videoEl);
syncStrategy.hls.on(Hls.Events.MANIFEST_PARSED, () => {});
videoEl.play();

LiveLike.init({ clientId, syncStrategy });
```

## Using Other Players

Other players can be used by implementing a custom Sync Strategy. LiveLike only supports syncing HLS streams because it depends on the [Program Date Time](https://tools.ietf.org/html/draft-pantos-http-live-streaming-13#section-3.4.5) metadata from the stream.

> 🚧 Other stream requirements
>
> See the [full list of stream requirements](doc:stream-requirements) to ensure sync works user-to-user and producer-to-user.

The custom sync strategy should extend the `ProgramDateTimeSyncStrategy` class and override the `programDateTime` getter. The getter must return a `Date` instance representing the Program Date Time from the stream. Consult your player's documentation for retrieving that information.

```javascript
/* Example code for creating and using a custom SyncStrategy */

import { ProgramDateTimeSyncStrategy } from '@livelike/engagementsdk';

export default class CustomSyncStrategy extends ProgramDateTimeSyncStrategy {
  constructor(customPlayer) {
    super(customPlayer);
    this.customPlayer = customPlayer;
  }

  get programDateTime() {
    /* Return a Date instance representing the Program Date Time of the stream */
    return this.customPlayer.getHlsProgramDateTime();
  }
}
```

Once you have a custom sync strategy, an instance of it can be pass to the SDK initialization step to use it:

```javascript
import CustomSyncStrategy from './custom-sync-strategy';

LiveLike.init({
  clientId,
  syncStrategy: new CustomSyncStrategy(customPlayer),
});
```

## Sending Messages Without Spoilers

The built-in chat elements will apply spoiler prevention to each message sent by default. If you want to send messages programmatically without spoilers, use the `LiveLike.sendMessage` method to send a message and include the spoiler timestamp in the `timestamp` parameter.

```javascript
LiveLike.sendMessage({
  message: 'Test message',
  roomId: 'example-room-id',
  // The timestamp value can be in the past
  // It only has to correspond with timecodes in the video stream
  timestamp: '2020-04-01T00:00:00Z'
})
```

> 📘 The `timestamp` argument corresponds to the `program_date_time` in the chat message data payloads.

## ES5 Compatible Custom Sync Strategy

If classes aren't available, a plain Object can be created. 

It must include a `currentTimecode` getter, and the getter must return a `Date` instance representing the Program Date Time from the stream. The object can contain any other logic necessary for obtaining the Program Date Time. Consult your player's documentation for retrieving that information.

```javascript
var customSyncStrategy = {
  get currentTimecode() {
    /* Return a Date representing the Program Date Time of the stream */
    return calculateCustomProgramDateTime()
  }
}

LiveLike.init({
  clientId,
  syncStrategy: customSyncStrategy
})
```
