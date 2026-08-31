---
title: Android SDK 3.0.17.2
author: Viktor Manev
hidden: false
published_at: '2026-07-31T15:23:27.862Z'
---
## What's fixed

- Fixed a `301` error when retrieving Application Config.

## Improvements

- Added `attributes` to `Comment.Author`.

- Added a public `commentId` property to `CommentReport`.

  You can still access the comment ID through `CommentReport.Comment.commentId`, but the new top-level property makes it easier to filter comment reports.

<br />