---
title: Android SDK 3.0.24
author: Viktor Manev
hidden: false
metadata:
  robots: noindex
published_at: '2026-10-19T15:20:30.547Z'
type: added
---
<br />

Added `sdk.preferAnonymousRequests` (default: `false`) to allow anonymous GET requests for `supported `comment APIs, including comments, replies, and counts.

```kotlin
sdk.preferAnonymousRequests = true
simpleCommentSession() // Create a session using anonymous comment reads.

sdk.preferAnonymousRequests = false
simpleCommentSession() // Create a session using authenticated comment read`s.

// Recreate the comment client, session, or feed client to apply changes.
// Existing instances keep the setting captured at creation.
```

#### Methods affected by `preferAnonymousRequests`:<br /><br /> Comment Client

```kotlin
val commentClient = sdk.comment(commentBoardId)
```

- `getComments()`
- `getCommentsPage()`
- `getCommentsCount()`
- `getComment()`
- `getCommentReplies()`
- `getCommentRepliesCount()`

## Comment Session

```kotlin
val commentSession = sdk.createCommentSession(commentBoardId)
```

- `loadHistory()`
- `loadNextHistory()`
- `loadPreviousHistory()`
- `reloadComments()`
- `openCommentReplies()`
- `getCommentReplies()`
- `getCommentReplyCount()`

The session's initial comment loading and comment-count requests also use anonymous reads.

## Comment Feed

```kotlin
val commentFeed = sdk.commentFeed()
```

- `getCommentsCount()`

## Important Notes

Writes, report reads, board reads, and profile operations remain authenticated. Recreate the client, session, or feed client after changing the setting.<br />

## More Info

[LiveLike : authenticated vs anonymous requests](https://docs.livelike.com/docs/comment-api-authenticated-vs-anonymous-requests)