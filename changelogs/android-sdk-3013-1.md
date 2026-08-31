---
title: Android SDK 3.0.14
author: Viktor Manev
hidden: false
published_at: '2026-06-25T16:26:52.603Z'
type: added
---
This release adds attribute support for chat messages, comments, and profiles. It also adds root-level reaction APIs for querying and counting reactions across multiple reaction spaces and targets and targetGroups alongside the socal graph update

## Attributes on chat messages, comments, and profiles

Chat messages, comments, and profiles now expose [attributes](https://docs.livelike.com/docs/data-integration-patterns#attributes). Added an `attributes` property to these objects:

- `LiveLikeChatMessage`
- `Comment`
- `LiveLikeProfile`

## Reactions

Added root-level `SDK.reaction()` reaction client singleton methods:

- `getUserReactions()` — query reactions across multiple reaction spaces using the `reactionSpaceIds` parameter.
- `getUserReactionsCount()` — count reactions across multiple reaction spaces using the `reactionSpaceIds` parameter.

The existing reaction session counterparts continue to work with a single reaction space ID.

## More info

- [Count user reactions across multiple spaces](https://docs.livelike.com/docs/reactions#count-user-reactions-across-multiple-spaces) SDK docs
- [List user reactions across multiple spaces](https://docs.livelike.com/docs/reactions#list-user-reactions-across-multiple-spaces) SDK docs
- [Get user reaction count](https://docs.livelike.com/reference/get-user-reaction-count) REST API docs

<br />

​