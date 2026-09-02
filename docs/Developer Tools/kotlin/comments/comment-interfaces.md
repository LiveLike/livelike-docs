---
title: Comment Interfaces
excerpt: Description of Android Comments Interfaces
deprecated: false
hidden: true
metadata:
  robots: index
---
<Callout icon="📘" theme="info">
  **CommentSession** <br />`val commentSession = SDK.createCommentSession(commentBoardId)`<br /><br />Requires a single `commentBoardId` to create an instance.<br />State manager for a comments screen. It maintains the current list of displayed comments, handles pagination as users scroll, and provides updated data for UI rendering.<br />Allows your UI to subscribe to `commentListFlow`, which always contains the current comment-feed state. It manages the initial load, loading more comments with `loadNextHistory(),` reloads, sorting, reply navigation, and updates to the displayed list.<br />----------------------------------------------------------------------------------------------------------------

  **CommentClient &#x20;**<br />`val commentClient =  SDK.comment("commentBoardID")`<br /><br />Requires a single `commentBoardId` to create an instance.<br />Performs individual comment API requests.<br /> Use it to perform specific operations—such as adding a comment, adding a reply, editing a comment, or fetching all replies—and receive results via callback.<br />----------------------------------------------------------------------------------------------------------------<br /><br />**CommentFeed**<br />`val commentFeed = SDK.commentFeed()`<br /><br />Works with one or more `commentBoardId` values passed to `getCommentsCount()`<br />Used fo&#x72;**&#x20;** counting comment across multiple Comment Boards in one request.
</Callout>

<br />

##
