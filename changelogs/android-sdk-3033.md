---
title: Android SDK 3.0.23
author: Viktor Manev
hidden: false
published_at: '2026-10-13T15:44:33.639Z'
type: added
---
# Added independent inline-reply sorting

Added independent inline-reply sorting through `inlineRepliesOrdering`, allowing newest-first top-level comments with oldest-first inline replies. Supported in:

- `LiveLikeCommentClient.getComments()` and `getCommentsPage()` through `GetCommentsRequestOptions`
- `LiveLikeKotlin.createCommentSession()` through its new `inlineRepliesOrdering` parameter

## InlineRepliesSorting

Added `InlineRepliesSorting` with seven supported values:

When `inlineRepliesOrdering` is omitted, inline replies follow the top-level comment sorting. Inline replies require `repliesLimit`.

<br />Sample:<br />CommentClient and CommentSession

```kotlin
commentClient.getComments(liveLikePagination = LiveLikePagination.FIRST,getCommentsRequestOptions = GetCommentsRequestOptions(sorting = CommentSortingOptions.NEWEST,repliesLimit = 3,inlineRepliesOrdering = InlineRepliesSorting.OLDEST))
```

```kotlin
val commentSession = sdk.createCommentSession
(
   commentBoardId ,
   withoutReportedThread = true, 
   inlineRepliesOrdering = CommentSortingOptions.NEWEST_REPLIES // NEW
 )
```