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
- `LiveLikeProfile`<br />
  ***

## Reactions

Added root-level `SDK.reaction()` reaction client singleton methods:<br />The existing `sdk.reactionSession()` API remains unchanged.

- `getUserReactions(request, callback)` — returns `UserReaction `records across multiple targets, target groups, and/or reaction spaces.

  **- Required:** at least one non-empty `reactionSpaceIds` or `targetGroupIds` list

  **- Optional:** `targetIds`, `reactionId`, `reactedById`, relationship filters, and pagination

- `getUserReactionsCount(request, callback)` — returns reaction totals per target.

  **- Required:** one `reactionSpaceId`

  **- Optional:** `targetIds`, `reactedById`, relationship filters, and pagination

  \- Supports multiple `targetIds`in one request<br />

  ***

  <br />`SDK.reaction() ` &#x20;

  -Added support for ad-hoc or batched queries across one or more reaction spaces, target groups, and targets.

  `SDK.reactionSession()`

  &#x20;\- Use when working within one configured reaction space.

***

## More info

- [Count user reactions across multiple spaces](https://docs.livelike.com/docs/reactions#count-user-reactions-across-multiple-spaces) SDK docs
- [List user reactions across multiple spaces](https://docs.livelike.com/docs/reactions#list-user-reactions-across-multiple-spaces) SDK docs
- [Get user reaction count](https://docs.livelike.com/reference/get-user-reaction-count) REST API docs

<br />

​