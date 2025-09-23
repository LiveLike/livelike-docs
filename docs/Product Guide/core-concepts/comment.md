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

<br />

## Creating a Comment Board

<br />

<details>
  <summary>Create Comment Board</summary>

  ```kotlin
  commentBoards.createCommentBoard(
              CreateCommentBoardRequestOptions(
                  customId = "",
                  title = "",
                  allowComments = true,
                  replyDepth = 1,
                  customData = "",
                  description = "",
                  contentFilter = "filtered"
              ),
              object : LiveLikeCallback<CommentBoard>() {
                  override fun onResponse(
                      result: CommentBoard?,
                      error: String?
                  ) {
                      result?.let {
                          //handle success
                      }
                      error?.let {
                          //handle error

                      }
                  }
              }
          )
  ```
  ```swift Swift
  let sdk: EngagementSDK

  let createBoardOptions = CreateCommentBoardRequestOptions(
    title: "",
    customID: "",
    allowComments: true,
    repliesDepth: 1
  )

  sdk.commentBoards.createCommentBoard(
    createCommentBoardOptions: createBoardOptions
  ) { result in
     switch result {
       case .success(let commentBoard):
       // handle success
       case .failure(let error):
       // handle failure
     }
  }
  ```
  ```javascript
  LiveLike.createCommentBoard({
    title: 'sd',
    customId: 'postid1',
    repliesDepth: 2,
    allowComments: true,
    description: 'desc',
    customData: 'abc',
    contentFilter: 'filtered'
  }).then((commentBoard) => console.log(commentBoard));
  ```
</details>

<br />

## Updating a Comment Board

<br />

<details>
  <summary>Update Comment Board</summary>

  ```kotlin
  commentBoards.updateCommentBoard(
              UpdateCommentBoardRequestOptions(
                  commentBoardId = "",
                  customId = "",
                  title = "",
                  allowComment = true,
                  replyDepth = 1,
                  customData = "",
                  description = "",
                  contentFilter = "filtered"
              ),
              object : LiveLikeCallback<CommentBoard>() {
                  override fun onResponse(
                      result: CommentBoard?,
                      error: String?
                  ) {
                      result?.let {
                          //handle success
                      }
                      error?.let {
                          //handle error

                      }
                  }
              }
          )
  ```
  ```swift Swift
  let sdk: EngagementSDK

  let updateBoardOptions = UpdateCommentBoardRequestOptions(
    title: "",
    customID: "",
    allowComments: true,
    repliesDepth: 1
  )

  sdk.commentBoards.updateCommentBoard(
    commentBoardID: "", 
    updateCommentBoardOptions: updateBoardOptions
  ) { result in
     switch result {
       case .success(let commentBoard):
       // handle success
       case .failure(let error):
       // handle failure
     }
   }
  ```
  ```javascript
  LiveLike.updateCommentBoard({
    commentBoardId: '5f5fea99-569b-42f3-875d-5b3943b64ba0',
    title: 'title',
    customId: 'postID431',
    repliesDepth: 1,
    allowComments: true,
    description: 'abc',
    customData: 'custom data',
    contentFilter: 'filtered'
  }).then((commentBoard) => console.log(commentBoard));
  ```
</details>

<br />

## Listing Comment Boards

<br />

<details>
  <summary>Update Comment Board</summary>

  ```kotlin
  commentBoards.getCommentBoards(
              LiveLikePagination.FIRST,
              object : LiveLikeCallback<List<CommentBoard>>() {
                  override fun onResponse(result: List<CommentBoard>?, error: String?) {
                      result?.let {
                          //handle success
                      }
                      error?.let {
                          //handle error

                      }
                  }
              }
          )
  ```
  ```swift
  let sdk: EngagementSDK

  sdk.commentBoards.getCommentBoards(
    page: .first
  ) { result in
     switch result {
       case .success(let commentBoards):
       // handle success
       case .failure(let error):
       // handle failure
     }
   }
  ```
  ```javascript
  LiveLike.getCommentBoards().then(({results}) => console.log(results))
  ```
</details>

<br />

## Deleting a Comment Board

<br />

<details>
  <summary>Delete Comment Board</summary>

  ```kotlin
  commentBoards.deleteCommentBoards(
      DeleteCommentBoardRequestOptions(commentBoardId = ""),
      object : LiveLikeCallback<LiveLikeEmptyResponse>() {
          override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {
              
          }
      }
  )
  ```
  ```swift Swift
  let sdk: EngagementSDK

  sdk.commentBoards.deleteCommentBoard(
    commentBoardID: ""
  ) { result in
     switch result {
       case .success:
       // handle succes
       case .failure(let error):
       // handle failure
     }
  }
  ```
  ```javascript
  LiveLike.deleteCommentBoard({
    commentBoardId: 'aa7e03fc-01f0-4a98-a2e0-3fed689632d7',
  }).then(({ results }) => console.log(results));
  ```
</details>

## Working with Comments

Comments APIs are accessed via the CommentClient in SDKs, linked to a specific comment board. For Web, APIs are available directly under LiveLike.

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

## Creating a Comment

<br />

<details>
  <summary>Creating a Comment</summary>

  ```kotlin
  commentClient.addComment(
              AddCommentRequestOptions(
                  text = "",
                  customData = "",
                  authorImageUrl = profileImageUrl
              ), object : LiveLikeCallback<Comment>() {
                  override fun onResponse(result: Comment?, error: String?) {
                      result?.let {
                          //handle success
                      }
                      error?.let {
                          //handle error

                      }
                  }
              }
          )
  ```
  ```swift
  let commentClient: CommentClient

  commentClient.addComment(
    text: "",
    authorImageURL: imageURL,
    customData: ""
  ) { result in
     switch result {
       case .success(let comment):
       // handle success
       case .failure(let error):
       // handle failure
     }
  }
  ```
  ```javascript
  LiveLike.addComment({
       text: '<Your text comment>',
       customData:'<Your custom data to send with reply comment>',
       commentBoardId:'<Your comment board Id>'
     }).then(comment => console.log(comment));
  ```
</details>

<br />

## Reply to a Comment

<br />

<details>
  <summary>Reply to a Comment</summary>

  ```kotlin
  commentClient.addCommentReply(
              AddCommentReplyRequestOptions(
                  parentCommentId = "",
                  text = "",
                  customData = "",
                  authorImageUrl = profileImageUrl
              ), object : LiveLikeCallback<Comment>() {
                  override fun onResponse(result: Comment?, error: String?) {
                      result?.let {
                          //handle success
                      }
                      error?.let {
                          //handle error

                      }
                  }
                  )
  ```
  ```swift
  let commentClient: CommentClient

  commentClient.addCommentReply(
    parentCommentID: "",
    text: "",
    authorImageURL: imageURL,
    customData: ""
  ) { result in
     switch result {
       case .success(let comment):
       // handle success
       case .failure(let error):
       // handle failure
     }
  }
  ```
  ```javascript
  LiveLike.addCommentReply({
       text: '<Your text comment>',
       customData: '<Your custom data to send with reply comment>',
       commentBoardId: '<Your comment board Id>',
       parentCommentId: '<Your parent  comment Id>'
  }).then(comment => console.log(comment));
  ```
</details>

<br />

## Get Comment

<br />

<details>
  <summary>Get Comment</summary>

  ```kotlin Kotlin
   commentClient.getComment(
      GetCommentRequestOptions(commentId=""),
      object : LiveLikeCallback<Comment>() {
          override fun onResponse(result: Comment?, error: String?) {
              result?.let {
                  //handle success
              }
              error?.let {
                  //handle error
              }
          }
          )
  ```
  ```swift Swift
  commentClient.getComment(commentID: String) { result in
     switch result {
       case .success(let comment):
       // handle success
       case .failure(let error):
       // handle failure
     }
  }
  ```
  ```javascript
  LiveLike.getComment({
     commentBoardId: "<comment-board-id>",
     commentId:"<comment-id>"})
    .then(({results}) => console.log(results))
  ```
</details>
