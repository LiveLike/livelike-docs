---
title: Android 3.0.27
author: Viktor Manev
hidden: true
published_at: '2026-11-20T16:59:13.910Z'
---
## Added sdk.profile().getUserComments() to retrieve comments posted by the current user across comment boards.<br /><br />

```kotlin
sdk.profile().getUserComments(
request = GetUserCommentsRequestOptions(
commentBoardId = "board-id",
ordering = UserCommentsSortingOptions.NEWEST
),
liveLikePagination = LiveLikePagination.FIRST
) { page, error ->
    val comments = page?.results
}
```

Optional parameters:

- commentBoardId: Limit results to one board.
- parentCommentId: Filter by parent comment.
- ordering: NEWEST (default) or OLDEST.
- topLevel: Filter by top-level status.
- withoutDeletedThread: Exclude deleted threads when true.
- liveLikePagination: FIRST (default), NEXT, or PREVIOUS.