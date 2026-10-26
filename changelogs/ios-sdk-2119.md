---
title: iOS SDK 2.119
author: LJupcho Nastevski
hidden: false
published_at: '2026-10-26T19:01:18.498Z'
type: added
---
Added new querry parameter to `GetCommentCountsRequestOptions` and `GetCommentsRequestOptions` - `excludeCommentReportThreshold` .

The parameter specifies the minimum number of reports a comment must receive to be excluded. A reported parent comment with replies remains visible so that its reply thread can still be rendered.<br />If omitted, no filtering is applied. The value must be a positive integer.

<br />

API Reference:

[https://docs.livelike.com/reference/list-comments](https://docs.livelike.com/reference/list-comments "https://docs.livelike.com/reference/list-comments")