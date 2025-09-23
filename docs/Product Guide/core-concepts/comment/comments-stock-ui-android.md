---
title: Comments Stock UI (Android)
excerpt: Comment UI is available from version 2.87
deprecated: false
hidden: false
metadata:
  robots: index
---
The Comments Stock UI is a powerful and flexible Android widget that allows developers to easily integrate a fully functional comment board and comment system into their Android applications. This widget comes packed with features such as sending and receiving comments, replying to comments, reacting to comments, and comprehensive moderation capabilities including reporting, blocking, and deleting comments. Additionally, developers can customize the appearance of the CommentView by utilizing custom theme attributes. CommentSession needs to be created to use comments stock UI

# Getting Started

## Installation

To integrate the CommentView into your Android application, follow these steps:

1. Adding CommentView to your Layout

   To use the CommentView, add it to your XML layout file:

   <details>
     <summary>Comment View</summary>

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
   </details>
