---
title: iOS SDK 2.116
author: LJupcho Nastevski
hidden: false
published_at: '2026-08-24T16:18:03.894Z'
---
- GetCommentsRequestOptions now has `excludeInactiveProfile` property, to filter out comments by inactive profiles;
- `Comment` has a new property called `isAuthorActive` - `bool` value representing if the author is active;
- Added `commentIDs` to `GetCommentReportsListRequestOptions` to allow filtering for multiple commentIDs. When making a request `commentID` is merged with `commentIDs` and duplicate values are removed;
- Fixed a bug that caused duplication of query parameters when getting next comments pages;

<br />

Additional information:

1. [https://docs.livelike.com/reference/list-comments](https://docs.livelike.com/reference/list-comments "https://docs.livelike.com/reference/list-comments")
2. [https://docs.livelike.com/reference/get-list-of-comment-reports](https://docs.livelike.com/reference/get-list-of-comment-reports "https://docs.livelike.com/reference/get-list-of-comment-reports")