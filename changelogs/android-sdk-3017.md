---
title: Android SDK 3.0.17.1
author: Viktor Manev
hidden: false
published_at: '2026-07-24T11:40:23.718Z'
type: fixed
---
## What's fixed<br />

&#x20;&#x20;

#### - Comments and replies returned by these APIs now correctly populate `isFromMe` and `isDeletedByMe`.

- Added ownership mapping with `withOwnership(...)` to:

  - `editComment(...)`
  - `addCommentReply(...)`

  Ownership mapping is also applied to all comments returned by commentClient:

  - `addComment(...)`
  - `getComments(...)`
  - `getCommentReplies(...)`
  - `getComment(...)`
  - `getCommentsPage(...)`

<br />