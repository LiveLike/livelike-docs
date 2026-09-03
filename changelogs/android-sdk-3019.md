---
title: Android SDK 3.0.19
author: Viktor Manev
hidden: false
published_at: '2026-09-01T15:14:50.196Z'
type: added
---
`repliesLimit` has been available through the existing `sdk.comment()` APIs since SDK version `3.0.16`<br /><br />**commentSession&#x20;**&#x63;an optionally include a small preview of replies beneath each top-level comment. This is useful for feeds that show a few replies inline.<br />

## Configuration

Configure the limit when creating the session:

```kotlin
val commentSession = sdk.createCommentSession(
  commentBoardId = commentBoardId,
  repliesLimit = 2
)
```

Or update it later:

```kotlin
commentSession.setRepliesLimit(2)
commentSession.reloadComments()
```

***

## Behaviour

- `repliesLimit` is optional. When it is null (the default), existing behaviour is unchanged and inline reply previews are not requested.
- Valid values are 1..5. Values outside this range throw `IllegalArgumentException`.
- The limit applies to top-level comment history loads:
  - initial session load
  - `loadNextHistory()`
  - `reloadComments()`
- Comments emitted through `commentListFlow` can include up to the configured number of preview replies in `Comment.replies`.
- The limit does not affect `getCommentReplies()`, which retrieves the full reply list for a selected comment.

more info : <Anchor target="_blank" href="https://docs.livelike.com/docs/comment-boards#get-a-list-of-replies-to-a-comment">docs.comments</Anchor><br /><br />available versions: `3.0.19` (ktor 3, default) and `3.0.19-ktor2`