---
title: Spoiler Prevention (Android)
excerpt: Preventing spoilers on Android
deprecated: false
hidden: false
metadata:
  title: Spoiler Prevention | Android SDK | LiveLike Developer Hub
  description: >-
    The Android SDK Spoiler Prevention features allows you to publish
    spoiler-free content with the Engagement SDK.
  robots: index
next:
  description: ''
---
## Enabling Sync

This feature enables you to publish spoiler-free content with the Engagement SDK. When enabled, all published content from the Producer Suite (see [Stream Requirements](https://docs.livelike.com/docs/stream-requirements)) and chat messages will be synced with Live video. Note that we don't currently support VOD. To enable sync, you will need to provide a value that represents the date/time of your media player's current playback position.

To enable sync, include a method to the `createSession` that returns the current live timecode.

```kotlin
val session = engagementSDK.createContentSession("<program-url>", object:LiveLikeSDK.TimecodeGetter{
  override fun getTimecode(): EpochTime {
    return EpochTime(player.bufferedPosition)
    }
})
```
```java
LiveLikeContentSession session = liveLikeSDK.createContentSession("<program-url>", new LiveLikeSDK.TimecodeGetter() {
  @NotNull
  @Override
  public EpochTime getTimecode() {
    return new EpochTime(player.getEpochTime());
  }
});
```

## ExoPlayer Sync Plugin

While the overriding mechanism described above is fairly simple, we also provide an [ExoPlayer](https://github.com/google/ExoPlayer) plugin that automatically handles the sync override. The plugin has the following stream prerequisites:

* Live HLS stream
* Stream contains the [EXT-X-PROGRAM-DATE-TIME]\([https://tools.ietf.org/html/rfc8216#section-](https://tools.ietf.org/html/rfc8216#section-)\
  4.3.2.6) tags in the HLS manifest

Add the following to your build.gradle to install the plugin:

`implementation 'com.livelike.android-engagement-sdk:pluginexoplayer:<<current-android-version>>'`

Once the session is initialized, you can pass your Exoplayer instance directly and get your HLS stream synchronized with widgets and chat. The plugin will get the timecode from the Program-Date-Time tags included in your HLS manifest.

```kotlin
val session = engagementSDK.createExoplayerSession(
  object : PlayerProvider {
    override fun get(): SimpleExoPlayer? {
      return getPlayer()
    }
  },
  "<program-url>"
)
```
```java
import static com.livelike.livelikepreintegrators.ExoplayerPreintegratorKt.createExoplayerSession;

LiveLikeContentSession session = createExoplayerSession(liveLikeSDK, () -> getPlayerInstance(), "<program-url>");
```
