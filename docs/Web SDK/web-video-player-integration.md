---
title: Video Player Integration
excerpt: Integrating the Web SDK with video players
deprecated: false
hidden: false
metadata:
  title: Video Player Integration | Web SDK | LiveLike
  description: >-
    The Engagement SDK is designed to work with all video players on the web,
    from basic `<video>` elements to your own custom player.
  robots: index
next:
  description: ''
---
The Engagement SDK is designed to work with all video players on the web, from basic `<video>` elements to your own custom player. Integrating the SDK with the video player is also optional, it's only needed to take advantage of advanced features like [Spoiler Prevention](doc:spoiler-free-sync), or if you want a more cohesive or customized experience.

> 👍 Looking for inspiration?
>
> Check out the [Layout Best Practices guide](doc:design-best-practices) for some ideas for how to arrange LiveLike features within your video experience.

## Video Overlays

One common use-case for the SDK is overlaying [widgets](doc:web-widgets) on top of a video. This can be accomplished with CSS positioning. Here is some sample code for overlaying [pop-up widgets](doc:web-widget-modes) in the top left of your player:

```html overlay.html
<div class="your-overlay-container">
  <video class="your-video-player"></video>
  <livelike-widgets programid="example-program-id"></livelike-widgets>
</div>
```
```css overlay.css
.your-overlay-container {
  position: relative;
}

.your-overlay-container livelike-widgets {
  position: absolute;
  top: 0; /* Align to top edge of player */
  left: 0; /* Align to left edge of player */
}
```

Video players can be much more complex in the wild, and so an integration in practice will probably be more sophisticated. There are some things to consider for a successful integration:

* Keep the [stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context) in mind
* If there will be more overlays on top of the LiveLike features, make sure that those features will still be clickable when the other overlays are not visible
* Use [Pointer Events](https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events) wisely when multiple overlays are displayed simultaneously

## Spoiler Prevention

The SDK can be used to prevent the audience from being spoiled by the producer and by each other.  This requires some JavaScript to accomplish. The SDK has built-in support for some common players like Hls.js, and you can add support for your own player if needed. Check out the [Spoiler Prevention for Web integration docs](doc:web-spoiler-free-sync) to learn more.

> 🚧 Note on Embedded Players
>
> The essential functionality of the SDK is available alongside embedded players like YouTube Live, Vimeo, and Twitch. However, without access to the timing information inside of the stream within the embedded player, advanced functionality like Spoiler Prevention is not supported.

## Embedded Players

Many stream hosting services allow embedding streams on other web pages. These services include:

* YouTube Live
* Vimeo
* Twitch

LiveLike features like widgets and chat work as expected alongside these players, though the limited nature of developer access to the internals of these hosted and embedded players constrains the depth of integration.

> 📘 Using an embedded player for your experience?
>
> Read the [YouTube Live Integration](youtube-live-integration-web-tutorial) tutorial for some ideas on how to integrate LiveLike with YouTube Live or another embedded player on your site.
