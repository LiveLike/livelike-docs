---
title: Android SDK 3.0.16
author: Viktor Manev
hidden: false
published_at: '2026-07-14T16:15:11.215Z'
---
## What's new

This release adds optional inline reply support to the low-level comment client APIs and improves how paged comment results handle ownership flags.

## Comments

- Added optional `repliesLimit` support to:
  - `sdk.comment(...).getComments(...)`
  - `sdk.comment(...).getCommentsPage(...)`

- Updated `Comment.replies`  so the SDK can distinguish between:
  - `null` — inline replies were not requested or were not returned.
  - `[]` — inline replies were requested, but no replies exist.

- When `repliesLimit` is provided, `Comment.replies` returns inline replies in the comment result. The response can include a minimum of `1` reply and a maximum of `5` replies per comment.

## Fixed

- Fixed a bug in `getCommentsPage(...)` where `isFromMe` and `isDeletedByMe` were not correctly set on paged comment results.

## Important note

`CommentSession` was intentionally left unchanged. `repliesLimit` is supported only on the low-level `sdk.comment(...)` client APIs, not on `createCommentSession(...)` or `LiveLikeCommentSession`.