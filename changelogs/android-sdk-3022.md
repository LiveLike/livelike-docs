---
title: Android SDK 3.0.22
author: Viktor Manev
hidden: false
published_at: '2026-09-25T14:07:10.065Z'
---
# Reported comments filtering

<br /><br />Added optional withoutReportedThread support. When true, reported comments without replies are excluded; reported parents with replies remain visible. Lists and counts use the same filtering rules.

## Supported APIs:

- **CommentClient**: `getComments()`, `getCommentsPage()`, `getCommentsCount()`, `getCommentReplies()`, `getCommentRepliesCount()`.
- **CommentFeed**: `getCommentsCount()`.
- **CommentSession**: configurable through `createCommentSession()`, applied to session comment/reply loading and counts.

Default behaviour remains unchanged when the option is ignored.