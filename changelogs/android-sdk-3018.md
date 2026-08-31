---
title: Android SDK 3.0.18
author: Viktor Manev
hidden: false
published_at: '2026-08-18T10:04:49.977Z'
type: added
---
### **Comments: inactive author filtering**

Added an opt-in `excludeInactiveProfile` option for comments and replies.

When enabled, the SDK sends `exclude_inactive_profile=true` and exposes `Comment.isAuthorActive` for retained comments whose author is inactive but whose replies must remain visible.

The option is available through `CommentClient`, `CommentSession`, and comment count requests. <br />Default behaviour is unchanged.<br /><br /><br />**Comment Reports**

- Added `commentIds: List<String>` to `GetCommentReportsRequestOptions` for retrieving reports for multiple comments in one request.
- Existing `commentId` remains available for backward compatibility and single-comment lookup.
- When both fields are supplied, IDs are combined and duplicates are removed.
- Use `CommentReport.commentId` and `reportedById` to determine whether the authenticated user can cancel a report.<br /><br />more info: [https://docs.livelike.com/docs/comment-report](https://docs.livelike.com/docs/comment-report "https://docs.livelike.com/docs/comment-report")<br /><br />