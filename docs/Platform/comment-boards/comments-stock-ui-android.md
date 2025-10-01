---
title: Comments Stock UI (Android)
excerpt: Comment UI is available from version 2.87
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Comments Stock UI is a powerful and flexible Android widget that allows developers to easily integrate a fully functional comment board and comment system into their Android applications. This widget comes packed with features such as sending and receiving comments, replying to comments, reacting to comments, and comprehensive moderation capabilities including reporting, blocking, and deleting comments. Additionally, developers can customize the appearance of the CommentView by utilizing custom theme attributes. CommentSession needs to be created to use comments stock UI

# Getting Started

## Installation

To integrate the CommentView into your Android application, follow these steps:

1. Adding CommentView to your Layout

   To use the CommentView, add it to your XML layout file:

```c xml
<com.livelike.ui.comments.CommentView
        android:id="@+id/commentview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5"
        app:profileImageUrl="https://images.mid-day.com/images/images/2021/oct/Dhoni-aa_d.jpg"
        app:commentViewTheme="@style/MyCustomCommentViewTheme"/> // For custom Theme (Optional)
```

## Features

### Sending and Receiving Comments

Users can easily send comments and reply on it. Comment System supports infinite reply depth and is controllable by integrator.

<Image align="center" width="300px" src="https://files.readme.io/cbd1a53-Screenshot_2023-09-11_at_5.47.16_PM.png" />

### Comment Replies

Users can reply to comments, creating threaded discussions.\
Nested replies are supported, offering a structured conversation.

<Image align="center" width="300px" src="https://files.readme.io/e423341-Screenshot_2023-09-11_at_5.48.51_PM.png" />

### Comment Reactions

Users can react to comments with emojis or custom reactions.\
Provides an expressive way for users to engage with content.

<Image align="center" width="400px" src="https://files.readme.io/443d908-Screenshot_2023-09-11_at_5.50.41_PM.png" />

### Sorting Filter

<Image align="center" width="400px" src="https://files.readme.io/056f43e-Screenshot_2023-09-11_at_5.51.05_PM.png" />

### Moderation

Comprehensive moderation tools for maintaining a safe and respectful environment.\
Features include reporting, blocking, and deleting comments.\
Profanity control helps maintain a clean and respectful conversation.

```asp Kotlin
While creating the CommentSession, you can choose what can be done for profane comments. You can pass:
  1- ProfaneComment.MASK (Shows *** for bad words)
  2- ProfaneComment.FILTERED (Whole comment containing bad word is removed)
  3- ProfaneComment.CUSTOM (with this you can pass a filteredTextForComment function which returns a String for replacing ***)
  
 //create comment session
createCommentSession(
    commentBoardId: String,
    profaneComment: ProfaneComment = ProfaneComment.CUSTOM,
    filteredTextForComment: ((Comment) -> String)?=null,
    delegate: CommentLocalCacheDelegate? = null
): LiveLikeCommentSession
        
See the Usage section for more clarity
       

```

<Image align="center" width="400px" src="https://files.readme.io/b98a56b-Screenshot_2023-09-11_at_5.50.16_PM.png" />

<Image align="center" width="400px" src="https://files.readme.io/35b86a2-Screenshot_2023-09-11_at_5.50.25_PM.png" />

### You can control profanity either by masking(\*\*\*) bad words in a comment or completely removing the comment.

<Image align="center" width="400px" src="https://files.readme.io/4fb3c74-Screenshot_2023-09-11_at_5.50.50_PM.png" />

### Customization

Developers can customize the appearance of the CommentView using custom theme attributes.\
Customize colors, backgrounds, positions, fonts, and more to fit your app's design.

## Usage

Create Comment Session. Additionally, enable reactions that can be integrated with the comments by creating reaction session using [create reaction space API](https://docs.livelike.com/docs/reactions) Attach the comment section to the comment view defined in the XML layout to ensure seamless interaction and user experience.

```java Kotlin
  //create comment session
commentSession =
    (application as LiveLikeApplication)
        .sdk
        .createCommentSession(commentBoardId, ProfaneComment.MASK)
  
  
  //create reaction session
 reactionSession =
    (application as LiveLikeApplication)
        .sdk
        .createReactionSession(reactionSpaceId, commentBoardId, errorDelegate)
  
  
//set the comment session to the comment view  
commentview.setSession(commentSession!!, reactionSession)                
```

## XML (Custom Theme Attributes)

```
<resources>
<style name="MyCustomCommentViewTheme">
        <item name="commentBackground">#FFFFFF</item>
        <item name="profileNameTextColor">#000000</item>
        <item name="profileTvTimeTextColor">#000000</item>
        <item name="commentBubbleBackgroundDrawable">@drawable/demo_comment_rounded_corner</item>
        <item name="commentTextColor">#000000</item>
        <item name="commentRepliesButtonColor">#3067F6</item>
        <item name="commentReactionButtonColor">@drawable/demo_emotion_smile</item>
        <item name="viewOrder">reactionFirst</item>
        <item name="reactionReplyButtonOrientation">horizontal</item>
        <item name="profileNameParentCommentTextColor">#000000</item>
        <item name="profileTvParentTimeTextColor">#000000</item>
        <item name="parentCommentTextColor">#000000</item>
        <item name="parentCommentRepliesButtonColor">#3067F6</item>
        <item name="parentCommentReactionButtonColor">@drawable/demo_emotion_smile</item>
        <item name="emptyViewBackground">#FFFFFF</item>
        <item name="emptyViewTextColor">#000000</item>
        <item name="emptyViewTextColorConv">#7A7B7C</item>
        <item name="emptyViewImageDrawable">@drawable/demo_emptycomments</item>
        <item name="sendViewBackground">#F6F8FA</item>
        <item name="editTextCommentDrawable">@drawable/demo_comment_edittext_rounded_corner</item>
        <item name="editTextCommentTextColor">#000000</item>
        <item name="replyBoxDrawable">@drawable/demo_reply_box_drawable</item>
        <item name="commentTotalCountBackground">#FFFFFF</item>
        <item name="commentTotalCountTextColor">#000000</item>
        <item name="replyTabLeftArrowImage">@drawable/demo_left_arrow</item>
        <item name="replyTabCrossImage">@drawable/demo_cross_button</item>
        <item name="commentCountTabImage">@drawable/baseline_mode_comment_24</item>
        <item name="filterHeaderTextColor">#000000</item>
        <item name="filterHeaderImage">@drawable/baseline_arrow_drop_down_24</item>
    </style>
</resources>
```

### Conclusion

The CommentView is a versatile and feature-rich solution for integrating a comment board and comment system into your Android application. It offers seamless customization options and provides a user-friendly experience for commenting, reacting, and moderating comments. By following this documentation, you can quickly and effectively implement this powerful widget into your project.
