---
title: Comment System Integration with Reaction Spaces
excerpt: >-
  This document provides a guide for integrating a comment system with reactions
  into your application using the provided APIs. The comment system allows users
  to interact with content by commenting on it, while reactions enable users to
  express their feelings or opinions on comments.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## 1\. Setting Up Comment Boards

### Purpose

Create containers for managing comments associated with specific content items.

### Steps

1. **Create Comment Board:**

   * Use the /api/v1/comment\_boards endpoint to create a comment board.
   * Provide a unique identifier (custom\_id) for the content item.
   * ```Text http
     POST /api/v1/comment_boards
     Content-Type: application/json

     {
         "custom_id": "blog_post_123"
     }
     ```

<br>

> 📘 See Also
>
> [Create Comment Board API](https://docs.livelike.com/reference/create-a-comment-board)

<br>

## 2\. Managing Comments

### Purpose

Allow users to post comments and retrieve comments associated with content items.

### Steps

1. **Post Comment:**

   * Use the /api/v1/comments endpoint to post a comment to a specific comment board.
   * Provide the board\_id and the comment text.
   * ```
     POST /api/v1/comments
     Content-Type: application/json

     {
         "comment_board_id": "board_id_123",
         "comment_text": "This is a great post!"
     }
     ```

<br>

> 📘 See also
>
> [Create a comment](https://docs.livelike.com/reference/create-a-comment)

## 3\. Setting up Reaction Space

### Purpose

Create spaces for managing reactions to comments.

### Steps

1. **Get Reaction Packs**
   * Use the /api/v1/reaction-packs/ endpoint to get list of available reaction packs for your application
     > 📘 See also
     >
     > [Reaction Pack API]()
2. **Create Reaction Space:**

* Use the /api/v1/reaction\_spaces endpoint to create a reaction space for a specific comment board.
* Provide the target\_group\_id as the board\_id and the reaction\_pack\_ids for the desired reaction packs.
* ```
  POST /api/v1/reaction_spaces
  Content-Type: application/json

  {
      "target_group_id": "board_id_123",
      "reaction_pack_ids": ["pack_id_1", "pack_id_2"]
  }
  ```

> 📘 See also
>
> [Create a reaction space](https://docs.livelike.com/reference/create-reaction-space)

## 4\. Interacting with Reactions

### Purpose

Allow users to react to comments and retrieve reaction counts.

### Steps

1. **Add Reaction to Comment:**

   * Use the /api/v1/user-reactions/ endpoint to add a reaction to a specific comment.
   * Provide the reaction\_space\_id, target\_id (comment ID), and the reaction\_id.
   * ```
     POST /api/v1/user_reactions
     Content-Type: application/json

     {
         "reaction_space_id": "space_id_123",
         "target_id": "comment_id_456",
         "reaction_pack_id": "pack_id_1"
     }

     ```
2. **Retrieve Reaction Counts:**
   * Use the /api/v1/user-reactions-count/ endpoint to retrieve reaction counts for specific comments.
   * Provide a list of target\_ids (comment IDs).
   * ```
     GET /api/v1/user-reactions-count/?target_id=comment_id_456&target_id=comment_id_789
     ```

<br>

> 📘 See also
>
> [Create a user reaction](https://docs.livelike.com/reference/create-a-user-reaction)

## 5\. Retrieving Comments and Reaction Counts

### Purpose

Fetch comments associated with a content item and retrieve reaction counts for each comment.

### Steps

1. **Retrieve Comments:**
   * Use the /api/v1/comments endpoint to retrieve comments associated with a specific comment board.
   * Provide the comment\_board\_id as a query parameter.
   * ```
     GET /api/v1/comments?comment_board_id=board_id_123
     ```
2. **Extract Comment IDs:**
   * Extract the comment\_id from each comment retrieved in the response.
3. **Retrieve Reaction Counts:**
   * Use the /api/v1/reactions\_count endpoint to retrieve reaction counts for each comment.
   * Provide a list of target\_ids (comment IDs) obtained in the previous step.
   * ```
     GET /api/v1/user-reactions-count/?target_id=comment_id_456&target_id=comment_id_789
     ```
4. **Map Reactions with Comments:**
   * Match the reaction counts obtained in the response with the corresponding comment IDs.
   * Display the comments along with their respective reaction counts in your application's interface.

# Conclusion

By following the steps outlined in this document, you can seamlessly integrate a comment system with reactions into your application. This will enhance user engagement and provide users with more ways to interact with your content. If you have any questions or need further assistance, please refer to the provided API documentation or reach out to our support team.