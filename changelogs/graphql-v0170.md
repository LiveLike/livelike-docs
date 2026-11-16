---
title: GraphQL v0.17.0
author: Akshay Garg
hidden: true
published_at: '2026-11-16T11:39:48.681Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This release introduces widgets Emoji Slider, Flair, and update on RBAC. Support for Apollo Cache Control.

### Release Changes


#### Apollo-compatible cache control for GraphQL Yoga

***

Support for Apollo Server's cache-control behavior to GraphQL Yoga.

#### Slider

***

* **emojiSlider**: Fetch an Emoji Slider widget by ID.
* **createEmojiSlider**: Create an Emoji Slider widget.
* **createEmojiSliderVote**: Vote on an Emoji Slider widget.
* **updateEmojiSliderVote**: Update a vote on an Emoji Slider widget.
* **publishEmojiSlider**: Publish an Emoji Slider widget.
* **deleteEmojiSlider**: Delete an Emoji Slider widget.