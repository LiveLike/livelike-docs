---
title: Comment
deprecated: false
hidden: false
metadata:
  robots: index
---
Use Comments to allow your audience to post their thoughts and reply to others on any feature or topic within your experience. The comments system supports threaded discussions, reactions, mentions, and moderation workflows to maintain safe and high-quality conversations.

## Comments Service

The Comments service enables app developers to add commenting functionality to any content in their experience. By creating comment boards and associating them with your content, users can post comments and replies.

**Sample Use Cases:**

* Blog post comments
* Video reactions
* Fan discussions of teams or events

## Glossary

* **Board**: Represents a topic or content area where users can post comments (e.g., blog post, video, sports match).
* **Comment**: A post made on a board. Comments can be top-level or replies to other comments.
* **Reply**: A comment in direct response to another comment.

## Working with Comment Boards in Swift and Kotlin

Comment Board functionality is accessed through the `CommentBoardClient` in the Swift and Kotlin SDKs.

```kotlin
val liveLikeEngagementSDK: EngagementSDK
val commentBoards = liveLikeEngagementSDK.commentBoard()
```
```swift Swift
let sdk: EngagementSDK
sdk.commentBoards
```

### Creating a Comment Board

> Create a new comment board where users can post comments and replies
>
> <details>
>   <summary>Create Comment Board</summary>
>
>   ```kotlin
>   commentBoards.createCommentBoard(
>               CreateCommentBoardRequestOptions(
>                   customId = "",
>                   title = "",
>                   allowComments = true,
>                   replyDepth = 1,
>                   customData = "",
>                   description = "",
>                   contentFilter = "filtered"
>               ),
>               object : LiveLikeCallback<CommentBoard>() {
>                   override fun onResponse(
>                       result: CommentBoard?,
>                       error: String?
>                   ) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift Swift
>   let sdk: EngagementSDK
>
>   let createBoardOptions = CreateCommentBoardRequestOptions(
>     title: "",
>     customID: "",
>     allowComments: true,
>     repliesDepth: 1
>   )
>
>   sdk.commentBoards.createCommentBoard(
>     createCommentBoardOptions: createBoardOptions
>   ) { result in
>      switch result {
>        case .success(let commentBoard):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.createCommentBoard({
>     title: 'sd',
>     customId: 'postid1',
>     repliesDepth: 2,
>     allowComments: true,
>     description: 'desc',
>     customData: 'abc',
>     contentFilter: 'filtered'
>   }).then((commentBoard) => console.log(commentBoard));
>   ```
> </details>

### Updating a Comment Board

> Modify the properties of an existing comment board, like title, replies depth, or description.
>
> <details>
>   <summary>Update Comment Board</summary>
>
>   ```kotlin
>   commentBoards.updateCommentBoard(
>               UpdateCommentBoardRequestOptions(
>                   commentBoardId = "",
>                   customId = "",
>                   title = "",
>                   allowComment = true,
>                   replyDepth = 1,
>                   customData = "",
>                   description = "",
>                   contentFilter = "filtered"
>               ),
>               object : LiveLikeCallback<CommentBoard>() {
>                   override fun onResponse(
>                       result: CommentBoard?,
>                       error: String?
>                   ) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift Swift
>   let sdk: EngagementSDK
>
>   let updateBoardOptions = UpdateCommentBoardRequestOptions(
>     title: "",
>     customID: "",
>     allowComments: true,
>     repliesDepth: 1
>   )
>
>   sdk.commentBoards.updateCommentBoard(
>     commentBoardID: "", 
>     updateCommentBoardOptions: updateBoardOptions
>   ) { result in
>      switch result {
>        case .success(let commentBoard):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>    }
>   ```
>   ```javascript
>   LiveLike.updateCommentBoard({
>     commentBoardId: '5f5fea99-569b-42f3-875d-5b3943b64ba0',
>     title: 'title',
>     customId: 'postID431',
>     repliesDepth: 1,
>     allowComments: true,
>     description: 'abc',
>     customData: 'custom data',
>     contentFilter: 'filtered'
>   }).then((commentBoard) => console.log(commentBoard));
>   ```
> </details>

### Listing Comment Boards

> Retrieve all comment boards available in your app.
>
> <details>
>   <summary>Update Comment Board</summary>
>
>   ```kotlin
>   commentBoards.getCommentBoards(
>               LiveLikePagination.FIRST,
>               object : LiveLikeCallback<List<CommentBoard>>() {
>                   override fun onResponse(result: List<CommentBoard>?, error: String?) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift
>   let sdk: EngagementSDK
>
>   sdk.commentBoards.getCommentBoards(
>     page: .first
>   ) { result in
>      switch result {
>        case .success(let commentBoards):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>    }
>   ```
>   ```javascript
>   LiveLike.getCommentBoards().then(({results}) => console.log(results))
>   ```
> </details>

### Deleting a Comment Board

> Remove a comment board and all associated comments.
>
> <details>
>   <summary>Delete Comment Board</summary>
>
>   ```kotlin
>   commentBoards.deleteCommentBoards(
>       DeleteCommentBoardRequestOptions(commentBoardId = ""),
>       object : LiveLikeCallback<LiveLikeEmptyResponse>() {
>           override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {
>               
>           }
>       }
>   )
>   ```
>   ```swift Swift
>   let sdk: EngagementSDK
>
>   sdk.commentBoards.deleteCommentBoard(
>     commentBoardID: ""
>   ) { result in
>      switch result {
>        case .success:
>        // handle succes
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.deleteCommentBoard({
>     commentBoardId: 'aa7e03fc-01f0-4a98-a2e0-3fed689632d7',
>   }).then(({ results }) => console.log(results));
>   ```
> </details>

<br />

## Comments & Moderation SDK Guide

The CommentClient allows you to manage comments in a Comment Board. It supports adding, replying, editing, deleting, reporting comments, and performing moderation actions.
For WebSDK, the APIs are available directly under LiveLike and do not require creating a CommentClient.

### Initialize CommentClient

```kotlin
private var commentClient: LiveLikeCommentClient? = null
commentClient = activeCommentBoard.id ? .let {
    commentBoardId - >
        liveLikeEngagementSDK.comment(
            commentBoardId
        )
}
```
```swift
let sdk: EngagementSDK

sdk.createCommentClient(
  for: ""
) { result in
   switch result {
     case .success(let commentClient):
     // store `commentClient` for later usage
     case .failure(let error):
     //handle failure
   }
}
```
```javascript
import LiveLike from "@livelike/engagementsdk";
```

<br />

### Creating a Comment

> Post a new comment to a comment board.
>
> <details>
>   <summary>Creating a Comment</summary>
>
>   ```kotlin
>   commentClient.addComment(
>               AddCommentRequestOptions(
>                   text = "",
>                   customData = "",
>                   authorImageUrl = profileImageUrl
>               ), object : LiveLikeCallback<Comment>() {
>                   override fun onResponse(result: Comment?, error: String?) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   commentClient.addComment(
>     text: "",
>     authorImageURL: imageURL,
>     customData: ""
>   ) { result in
>      switch result {
>        case .success(let comment):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.addComment({
>        text: '<Your text comment>',
>        customData:'<Your custom data to send with reply comment>',
>        commentBoardId:'<Your comment board Id>'
>      }).then(comment => console.log(comment));
>   ```
> </details>

### Reply to a Comment

> Respond to an existing comment on a comment board.
>
> <details>
>   <summary>Reply to a Comment</summary>
>
>   ```kotlin
>   commentClient.addCommentReply(
>               AddCommentReplyRequestOptions(
>                   parentCommentId = "",
>                   text = "",
>                   customData = "",
>                   authorImageUrl = profileImageUrl
>               ), object : LiveLikeCallback<Comment>() {
>                   override fun onResponse(result: Comment?, error: String?) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>
>                       }
>                   }
>                   )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   commentClient.addCommentReply(
>     parentCommentID: "",
>     text: "",
>     authorImageURL: imageURL,
>     customData: ""
>   ) { result in
>      switch result {
>        case .success(let comment):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.addCommentReply({
>        text: '<Your text comment>',
>        customData: '<Your custom data to send with reply comment>',
>        commentBoardId: '<Your comment board Id>',
>        parentCommentId: '<Your parent  comment Id>'
>   }).then(comment => console.log(comment));
>   ```
> </details>

### Get Comment

> Retrieve a specific comment by ID.
>
> <details>
>   <summary>Get Comment</summary>
>
>   ```kotlin Kotlin
>    commentClient.getComment(
>       GetCommentRequestOptions(commentId=""),
>       object : LiveLikeCallback<Comment>() {
>           override fun onResponse(result: Comment?, error: String?) {
>               result?.let {
>                   //handle success
>               }
>               error?.let {
>                   //handle error
>               }
>           }
>           )
>   ```
>   ```swift Swift
>   commentClient.getComment(commentID: String) { result in
>      switch result {
>        case .success(let comment):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.getComment({
>      commentBoardId: "<comment-board-id>",
>      commentId:"<comment-id>"})
>     .then(({results}) => console.log(results))
>   ```
> </details>

### Get Top-Level Comments

Fetch all top-level comments with optional filters.

> Filters: NEWEST, OLDEST, OLDEST_REPLIES, NEWEST_REPLIES, repliedSince, repliedUntil, isReported
>
> <details>
>   <summary>Get Comment</summary>
>
>   ```kotlin
>
>           commentClient.getComments(
>               GetCommentsRequestOptions(
>                   CommentSortingOptions.NEWEST,
>                   CommentSortingOptions.NEWEST_REPLIES,
>                   topLevel = true,
>                   withoutDeletedThread = true
>                           repliedSince =""
>               ),
>               LiveLikePagination.FIRST,
>               object : LiveLikeCallback<List<Comment>>() {
>                   override fun onResponse(
>                       result: List<Comment>?,
>                       error: String?
>                   ) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   let options = GetCommentRequestOptions(
>     orderBy: .newest, 
>     topLevel: true,
>     repliedSince: nil,
>     repliedUntil: nil,
>     since: nil,
>     until: nil
>   )
>
>   commentClient.getCommentsList(
>     page: .first,
>     options: options
>   ) { result in
>      switch result {
>        case .success(let comments):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.getComments({
>        commentBoardId:'<comment-board-id>',
>        sorting:'<Your comment sorting enum value>',
>        topLevel: true,
>        repliedSince:'2023-12-19T15:28:46.493Z',
>        repliedUntil:'2023-12-19T15:28:46.493Z',
>        since:'2023-08-22T14:30:45.123Z',
>        until:'2023-08-22T14:30:45.123Z',
>        isReported: true,
>        excludeDeletedCommentWithNoReplies: true,
>     }).then(commentBoard => console.log(commentBoard));
>   ```
> </details>

### Get Replies to a Comment

> Retrieve all replies for a specific comment.
>
> <details>
>   <summary>List of replies to a Comment</summary>
>
>   ```kotlin
>    commentClient.getCommentReplies(
>               GetCommentRepliesRequestOptions(commentId = “”,
>           withoutDeletedThread = true
>           CommentSortingOptions.NEWEST),
>           LiveLikePagination.FIRST,
>           object : LiveLikeCallback<List<Comment>>() {
>               override fun onResponse(
>                   result: List<Comment>?,
>                   error: String?
>               ) {
>                   result?.let {
>                       //handle success
>                   }
>                   error?.let {
>                       //handle error
>                   }
>               }
>           }
>           )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   let options = GetCommentRepliesListRequestOptions(
>     commentBoardID: "", 
>     parentCommentID: ""
>   )
>
>   commentClient.getCommentRepliesList(
>     options: options, 
>     page: .first
>   ) { result in
>      switch result {
>        case .success(let comments):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.getCommentReplies({
>        commentBoardId:'<comment-board-id>',
>        commentId:'<comment-id>',
>        sorting: LiveLike.CommentSort.NEWEST,
>        since:'2023-08-22T14:30:45.123Z',
>        until:'2023-08-22T14:30:45.123Z',
>        excludeDeletedCommentWithNoReplies: true,
>     }).then(comments => console.log(comments));
>   ```
> </details>

### Edit a Comment

> Update the text of an existing comment.
>
> <details>
>   <summary>Edit a Comment</summary>
>
>   ```kotlin
>     commentClient.editComment(
>               UpdateCommentRequestOptions(
>                   commentId = "", text = ""
>               ),
>               object : LiveLikeCallback<Comment>() {
>                   override fun onResponse(
>                       result: Comment?,
>                       error: String?
>                   ) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   commentClient.editComment(
>     commentID: "",
>     text: ""
>   ) { result in
>      switch result {
>        case .success(let comment):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.editComment({
>      commentBoardId: "<comment-board-id>",
>      commentId: "<comment-id>",
>      text: '<Your text comment>',
>      customData: '<Your custom data to send with reply comment>',
>   }).then(comment => console.log(comment))
>   ```
> </details>

### Delete a Comment

> Remove a comment from the board.
>
> <details>
>   <summary>Delete a Comment</summary>
>
>   ```kotlin
>     commentClient.deleteComment(
>               DeleteCommentRequestOptions(
>                   commentId = ""
>               ),
>               object : LiveLikeCallback<LiveLikeEmptyResponse>() {
>                   override fun onResponse(
>                       result: LiveLikeEmptyResponse?,
>                       error: String?
>                   ) {
>                       result?.let {
>                           //handle success
>                       }
>                       error?.let {
>                           //handle error
>                       }
>                   }
>               }
>           )
>   ```
>   ```swift
>   let commentClient: CommentClient
>
>   commentClient.deleteComment(
>     commentID: ""
>   ) { result in
>      switch result {
>        case .success(let comment):
>        // handle success
>        case .failure(let error):
>        // handle failure
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.deleteComment({
>      commentBoardId: "<comment-board-id>",
>      commentId: "<comment-id>"
>   })
>   ```
> </details>

<br />

## Moderating Comment Boards

### Create Comment Board Ban

Moderators can ban a profile to restrict its access in a comment board but the banned profile does not lose access to moderation tools if they have that.

> 1. profile_id: required,
> 2. comment_board_id: optional, if not provided, the profile will be banned from all the comment boards in the application, provided the moderator has sufficient permissions to do that.
> 3. description: optional, this field can be used to provide additional information about a ban or the reason for banning a user.
>
> <details>
>   <summary>Create Comment Board Ban</summary>
>
>   ```kotlin
>   commentBoards.createCommentBoardBan(
>       CreateCommentBanRequestOptions(
>           profileId="",
>           commentBoardId=""),
>           description="")
>       ),
>       object : LiveLikeCallback<CommentBoardBanDetails>() {
>           override fun onResponse(result: CommentBoardBanDetails?, error: String?) {
>               showToast(error, "comment board ban")
>               showToast(result?.toString(), "comment board ban")
>           }
>       }
>   )
>   ```
>   ```javascript
>   LiveLike.createCommentBoardBan({
>     profileId: '<profile_id>',
>     commentBoardId: '<comment_board_id>',
>     description: '<Reason for banning>',
>   }).then((commentBoardBan) => console.log(commentBoardBan));
>   ```
>   ```swift
>   let createCommentBoardBanOptions = CommentBoardBanRequestOptions(
>         commentBoardID: commentBoardID,
>         description: description
>   )
>           
>   sdk.commentBoards.createCommentBoardBan(
>         profileID: profileID, 
>         options: createCommentBoardBanOptions
>   ) { result in
>         switch result {
>         case .success(let commentBoardBan):
>             //Success block
>         case .failure(let error):
>             //Failure Block
>         }
>   }
>   ```
> </details>

### List Comment Board Bans

Get a list of comment board bans in an Application. Each comment board ban resource represents restrictive access to the comment board for a given user profile.

> 1. As a producer or privileged user I can see all the comment-board-ban-profile from the application
> 2. As a moderator, I can get a list of all comment-board-ban-profile for the comment boards where I am a moderator
> 3. As a normal profile, I will get a list of comment-board-ban-profile for myself only.
>
> <br />
>
> <details>
>   <summary>List Comment Board Ban</summary>
>
>   ```kotlin
>   commentBoards.getCommentBoardBans(
>       ListCommentBoardBanRequestOptions(
>           profileId="",
>           commentBoardId="")
>       ),
>       LiveLikePagination.FIRST,
>       object : LiveLikeCallback<List<CommentBoardBanDetails>>() {
>           override fun onResponse(result: List<CommentBoardBanDetails>?, error: String?) {
>               showToast(error, "comment board ban")
>               showToast(result?.toString(), "comment board ban list")
>           }
>       }
>   )
>   ```
>   ```javascript
>   LiveLike.getCommentBoardBans({
>     profileId: '<profile_id>',
>     commentBoardId: '<comment_board_id>',
>   }).then((paginatedResponse) => console.log(paginatedResponse));
>   ```
>   ```swift
>   let options = GetCommentBoardBansListRequestOptions(
>         profileID: profileID,
>         commentBoardID: commentBoardID
>   )
>           
>   sdk.commentBoards.getCommentBoardBans(
>         page: .first,
>         options: options
>   ) { result in
>         switch result {
>         case .success(let commentBoardBans):
>             //Success Block
>         case .failure(let error):
>             //Failure Block
>         }
>   }
>   ```
> </details>

### Get Comment Board Ban

> Get details of a specific ban.
>
> <details>
>   <summary>Get Comment Board Ban</summary>
>
>   ```kotlin
>   commentBoards.getCommentBoardBan(
>       GetBanDetailsRequestOptions(commentBoardBanId=""),
>       object : LiveLikeCallback<CommentBoardBanDetails>() {
>           override fun onResponse(result: CommentBoardBanDetails?, error: String?) {
>               showToast(error, "ban detail not found!")
>               showToast(result?.toString(), "comment board ban detail")
>           }
>       }
>   )
>   ```
>   ```javascript
>   LiveLike.getCommentBoardBan({
>     commentBoardBanId: '<comment_board_ban_id>',
>   }).then((commentBoardBan) => console.log(commentBoardBan));
>   ```
>   ```swift
>   sdk.commentBoards.getCommentBoardBanDetails(commentBoardBanID: banDetailsID) { result in
>         switch result {
>         case .success(let commentBoardBan):
>             //Success Block
>         case .failure(let error):
>             //Failure Block
>         }
>   }
>   ```
> </details>

### Delete Comment Board Ban

Remove a ban from a profile.

> A profile with moderation tools can unban himself if its get banned by other moderation access profile.
>
> <details>
>   <summary>Delete Comment Board Ban</summary>
>
>   ```kotlin
>   commentBoards.deleteCommentBoardBan(
>       DeleteCommentBanRequestOption(binding.commentBoardBanId.text.toString().trim()),
>       object : LiveLikeCallback<LiveLikeEmptyResponse>() {
>           override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {
>               error?.let { showToast(error, "delete comment board ban") }
>               result?.let { showToast("Deleted:", "comment board ban deleted") }
>           }
>       }
>   )
>   ```
>   ```javascript
>   LiveLike.deleteCommentBoardBan({
>     commentBoardBanId: '<comment_board_ban_id>',
>   })
>   ```
>   ```swift
>   sdk.commentBoards.deleteCommentBoardBan(commentBoardBanID: banDetailsID) { result in
>         switch result {
>         case .success:
>             //Success Block
>         case .failure(let error):
>             //Failure Block
>         }
>   }
>   ```
> </details>

### Create Comment Report

> Report a comment to moderators.
>
> <details>
>   <summary>Create Comment report</summary>
>
>   ```kotlin Kotlin
>   commentClient?.createCommentReport(
>       CreateCommentReportRequestOptions(
>           commentId="",
>           description = "",
>       ),
>       object : LiveLikeCallback<CommentReport>() {
>           override fun onResponse(result: CommentReport?, error: String?) {
>
>               result?.let {
>                   showToast(result?.toString(), result?.reportStatus!!)
>                   activeCommentReport = result
>               }
>
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>   ```
>   ```swift
>   commentClient.createCommentReport(
>   	commentID: commentID,
>     options: CreateCommentReportRequestOptions(
>     	description: descriptiontext
>     )
>   ) { result in
>      switch result {
>        case .success(let commentReport):
>            //Success Block
>        case .failure(let error):
>            //Failure Block
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.createCommentReport({
>     commentId: '<comment_id>',
>     description: '<Reason for reporting>',
>   }).then((commentReport) => console.log(commentReport));
>   ```
> </details>

### Get Comment Report

> Retrieve details of a specific report.
>
> <details>
>   <summary>Get Comment report</summary>
>
>   ```kotlin kotlin
>   commentClient?.getCommentReportDetail(
>       GetCommentReportDetailRequestOptions(commentReportId = ""),
>       object : LiveLikeCallback<CommentReport>() {
>           override fun onResponse(result: CommentReport?, error: String?) {
>               result?.let { showToast(result.toString(), "Current Report") }
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>   ```
>   ```swift
>   client.getCommentReportDetails(
>     commentReportID: commentReportID
>   ) { result in
>      switch result {
>        case .success(let commentReport):
>        			//Success Block
>        case .failure(let error):
>             //Failure Block
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.getCommentReport({
>     commentReportId: '<comment_report_id>',
>   }).then((commentReport) => console.log(commentReport));
>   ```
> </details>

### List Comment Reports

> Get all reports for a comment or board.
>
> <details>
>   <summary>Get Comment report</summary>
>
>   ```kotlin Kotlin
>   commentClient?.getCommentReports(
>       GetCommentReportsRequestOptions(
>           commentId = activeComment?.id!!,
>           ReportStatusOptions.PENDING,
>           commentBoardId = ""
>       ),
>       LiveLikePagination.FIRST,
>       object : LiveLikeCallback<List<CommentReport>>() {
>           override fun onResponse(result: List<CommentReport>?, error: String?) {
>               result?.let { showToast(result.toString(), result?.size.toString()) }
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>   ```
>   ```swift
>   commentClient.getCommentReports(
>     page: .first, 
>     options: .init(
>       commentBoardID: commentBoardID, 
>       commentID: nil, 
>       reportStatus: .dismissed
>     )
>   ) { result in
>      switch result {
>        case .success(let commentReports):
>        			//Success Block
>        case .failure(let error):
>             //Failure Block
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.getCommentReports({
>     commentBoardId: '<comment_board_id>',
>     commentId: '<comment_id>',
>     reportStatus: LiveLike.CommentReportStatus.PENDING,
>   }).then((paginatedResponse) => console.log(paginatedResponse));
>   ```
> </details>

### Delete Comment Report

> Delete a comment report.
>
> <details>
>   <summary>Delete Comment Report</summary>
>
>   ```kotlin Kotlin
>   commentClient?.deleteCommentReport(
>       DeleteCommentReportRequestOptions(commentReportId=""),
>       object : LiveLikeCallback<LiveLikeEmptyResponse>() {
>           override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {
>               result?.let { showToast(result.toString(), "Report Deleted") }
>
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>       
>
>   ```
>   ```swift
>   commentClient.deleteCommentReport(
>     commentReportID: commentReportID
>   ) { result in
>      switch result {
>        case .success:
>        			self.showAlert(title: "Comment Report Deleted", 
>                            message: "Comment Report Id: \(commentReportID)")
>        case .failure(let error):
>        			self.showAlert(title: "Error", message: error.localizedDescription)
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.deleteCommentReport({
>     commentReportId: '<comment_report_id>',
>   })
>   ```
> </details>

### Dismiss Comment Report

> Dismiss a specific report.
>
> <details>
>   <summary>Dismiss Comment Report</summary>
>
>   ```kotlin Kotlin
>   commentClient?.dismissCommentReport(
>       DismissCommentReportRequestOptions(commentReportId=""),
>       object : LiveLikeCallback<CommentReport>() {
>           override fun onResponse(result: CommentReport?, error: String?) {
>               result?.let { showToast(result.toString(), "Report Dismissed") }
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>       
>
>   ```
>   ```swift
>   commentClient.dismissCommentReport(
>     commentReportID: commentReportID
>   ) { result in
>      switch result {
>        case .success(let reportDetail):
>        			self.showAlert(title: "Comment Report Dismissed", 
>                            message: "Report Status: \(String(describing: reportDetail.reportStatus))")
>        case .failure(let error):
>        			self.showAlert(title: "Error", message: error.localizedDescription)
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.dismissCommentReport({
>     commentReportId: '<comment_report_id>',
>   }).then((commentReport) => console.log(commentReport));
>   ```
> </details>

### Dismiss All Comment Reports

> Dismiss all reports for a comment.
>
> <details>
>   <summary>Dismiss Comment Report</summary>
>
>   ```kotlin kotlin
>   commentClient?.dismissAllCommentReports(
>       DismissAllReportsForACommentRequestOptions(commentId=""),
>       object : LiveLikeCallback<DismissAllReports>() {
>           override fun onResponse(result: DismissAllReports?, error: String?) {
>               result?.let { showToast(result.toString(), "All Report Dismissed") }
>               error?.let { showToast(error, "Error!!") }
>           }
>       }
>   )
>       
>
>   ```
>   ```swift
>   commentClient.dismissAllCommentReports(
>     commentID: commentID
>   ) { result in
>      switch result {
>        case .success(let reportDetail):
>        			self.showAlert(title: "Report Dismissed", 
>                            message: "Report Status: \(String(describing: reportDetail.detail))")
>        case .failure(let error):
>        			self.showAlert(title: "Error", message: error.localizedDescription)
>      }
>   }
>   ```
>   ```javascript
>   LiveLike.dismissAllCommentReports({
>     commentBoardId: '<comment_board_id>',
>     commentId: '<comment_id>',
>   })
>   ```
> </details>
