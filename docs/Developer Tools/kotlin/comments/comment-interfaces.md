---
title: Comment Interfaces
excerpt: Description of Android Comments Interfaces
deprecated: false
hidden: false
metadata:
  robots: index
---
## **CommentBoard**

```
val commentBoardClient = SDK.commentBoard()
```

CommentBoardClient is used to manage Comment Boards themselves—not the individual comments inside a board. Think of a Comment Board as the container for a conversation. Create a board first, then use its id with `SDK.comment(commentBoardId)` or `SDK.createCommentSession(commentBoardId)` to work with comments.

Use CommentBoardClient to:

- Create, update, retrieve, list, and delete Comment Boards
- Retrieve board details before displaying or configuring a comments experience
- Moderate a board by creating, listing, retrieving, and removing profile bans
- Paginate lists of boards and board bans with LiveLikePagination

Comment Board operations are intended for board setup and moderation. To load, post, edit, delete, or reply to comments within one board, use CommentClient or CommentSession instead.<br /><br />

***

## **CommentClient**

```
val commentClient = SDK.comment("commentBoardID")
```

Requires a single commentBoardId to create an instance.
CommentClient performs direct, individual comment API requests and returns each result through a callback. Use it when you need to perform a specific action rather than manage a continuously updated comments screen.
It supports:

- Adding, retrieving, editing, and deleting comments.
- Loading comments with pagination, including getCommentsPage() when you need the total count and next/previous page URLs.
- Getting a comment or comment count.
- Adding replies, loading a comment’s full reply list, and getting its reply count.
- Moderation operations: creating, retrieving, dismissing, and deleting comment reports.
- Retrieving reports for one or more comments.
  Use CommentClient for actions such as submitting a comment, opening a full replies screen, reporting inappropriate content, or building a custom comment UI.
  For a stateful comment-feed UI with pagination and live updates, use CommentSession instead.<br /><br />
  ***


## **CommentSession**

```
val commentSession = SDK.createCommentSession(commentBoardId)
```

Requires a single commentBoardId to create an instance.
CommentSession is the state manager for a comments screen. Use it when your UI needs a continuously maintained comment feed, rather than making individual callback-based requests.
Subscribe to commentListFlow to receive the current list of comments whenever it changes. The session manages:

- The initial comment-history load.
- Pagination as the user scrolls with loadNextHistory().
- Refreshing the visible feed with reloadComments().
- Updating comment sorting with setCommentSorting().
- Opening and loading a selected comment’s replies with openCommentReplies().
- Returning from replies to the top-level feed with closeCommentReplies().
- Sending a top-level comment or a reply with sendComment(), depending on the current reply context.
- Optional inline reply previews through repliesLimit / setRepliesLimit().
  Use CommentSession for a standard comments UI with pagination and live updates. Use CommentClient instead for one-off operations such as reporting, editing, deleting, or fetching a specific comment.

***

## **CommentFeed**

```
val commentFeed = SDK.commentFeed()
```

Works with one or more `commentBoardId` values passed to `getCommentsCount()`.

Used for counting comments across multiple Comment Boards in one request.

***

##
