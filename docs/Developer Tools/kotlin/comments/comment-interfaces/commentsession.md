---
title: CommentSession
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
CommentSession manages the state of one Comment Board for a comments screen. Subscribe to its flows to render the current screen state, then call its methods as the user scrolls, opens a thread, posts, or moderates content.

## Create a session - Constructor parameters<br />

```kotlin
val commentSession = SDK.createCommentSession(
    commentBoardId = commentBoardId
 )
```

| Parameter              | Required | Description                                                                                                                         |
| ---------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| commentBoardId         | Yes      | The Comment Board to load.                                                                                                          |
| profaneComment         | No       | Profanity-filter behavior. Defaults to FILTERED.                                                                                    |
| filteredTextForComment | No       | Provides replacement text for filtered comments.                                                                                    |
| delegate               | No       | Local cache delegate for comment data.                                                                                              |
| excludeInactiveProfile | No       | When true, excludes inactive-profile comments where possible and marks thread-preserving comments appropriately. Defaults to false. |
| repliesLimit           | No       | Number of inline reply previews per top-level comment. null disables previews; valid values are 1–5.                                |

## Observe screen state

| Flow                        | Value                 | Use it for                                                                              |
| --------------------------- | --------------------- | --------------------------------------------------------------------------------------- |
| commentListFlow             | List<comment>         | Rendering the current top-level comments or currently open reply thread.                |
| commentsLoadedFlow          | Boolean               | Showing or hiding a loading state.                                                      |
| commentCountFlow            | Int                   | Showing the total comment count.                                                        |
| topCommentFlow              | Comment?              | Knowing which top-level comment's replies are currently open. null means the main feed. |
| commentsReplyCountFlow      | Int                   | Showing the reply count for the open thread.                                            |
| commentSortFlow             | CommentSortingOptions | Reflecting the active sort option.                                                      |
| commentSortByReactionIDFlow | String?               | Reflecting the reaction ID used for reaction-based sorting.                             |
| commentsReportsListFlow     | List<commentreport>   | Building moderation/reporting UI.                                                       |
| commentsBlockedListFlow     | List<blockedinfo>     | Building blocked-profile UI.                                                            |

## Load and navigate comments

| Method                      | Description                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------- |
| loadNextHistory()           | Loads the next page of the current feed or reply thread. Use for infinite scroll.   |
| loadPreviousHistory()       | Loads the previous page, when applicable.                                           |
| loadHistory(pagination)     | Loads comments using explicit pagination options.                                   |
| reloadComments()            | Clears the displayed top-level list and loads the first page again.                 |
| openCommentReplies(comment) | Opens the reply thread for a comment. Pass null to load the top-level comment feed. |
| closeLastCommentReplies()   | Goes back one level in the reply-navigation stack.                                  |
| closeAllCommentReplies()    | Returns to the top-level comment feed.                                              |
| isTopComment(comment)       | Returns whether a comment is a top-level comment.                                   |
| isReplyAllowed()            | Returns whether a reply can be added in the current context.                        |

## Configure the displayed feed

| Method                                        | Description                                                                                                                          |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| setCommentSortingOption(sortingOption)        | Changes the selected sort order for future loads. Call reloadComments() to refresh the current list.                                 |
| setCommentSortingReactionIDOption(reactionId) | Configures reaction-based sorting for future loads. Call reloadComments() afterwards.                                                |
| setRepliesLimit(repliesLimit)                 | Sets 1–5 inline reply previews for each top-level comment on future loads. Use null to disable previews, then call reloadComments(). |

## Send and moderate comments

| Method                                           | Description                                                        |
| ------------------------------------------------ | ------------------------------------------------------------------ |
| sendComment(...)                                 | Posts a top-level comment, or a reply when a reply thread is open. |
| reportComment(commentId, callback)               | Reports a comment.                                                 |
| unReportComment(commentReportId, callback)       | Removes the current user's report.                                 |
| deleteComment(commentId, callback)               | Deletes a comment.                                                 |
| getCommentReports()                              | Refreshes the session's reports flow.                              |
| getCommentReplyCount(commentId, callback)        | Gets a specific comment's reply count.                             |
| getCommentReplies(options, pagination, callback) | Makes a direct, callback-based request for replies.                |
| blockUser(profileId, callback)                   | Blocks a profile.                                                  |
| unBlockUser(profileId, callback)                 | Removes a profile block.                                           |
| getBlockedProfileList()                          | Refreshes the blocked-profiles flow.                               |
| getCommentBoard(callback)                        | Retrieves the current Comment Board details.                       |
| close()                                          | Releases the session when the screen is no longer needed.          |

## Basic usage

```kotlin
val commentSession = SDK.createCommentSession(
    commentBoardId = commentBoardId,
    repliesLimit = 2,
)

lifecycleScope.launch {
    commentSession.commentListFlow.collect { comments ->
        adapter.submitList(comments)
    }
}
```

### Load another page when the user reaches the end of the list:

```kotlin
commentSession.loadNextHistory()
```

### Change inline reply previews and refresh the visible feed:

```kotlin
commentSession.setRepliesLimit(3)
commentSession.reloadComments()
```

### Open replies for a selected comment:

```kotlin
commentSession.openCommentReplies(comment)
```

### Release the session when the screen is destroyed:

```kotlin
commentSession.close()
```
