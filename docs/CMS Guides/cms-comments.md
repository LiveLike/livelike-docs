---
title: Comments
excerpt: Managing comments using CMS
deprecated: false
hidden: false
link:
  new_tab: true
  url: https://scribehow.com/page/Untitled__o-qanyMDT3mffWyl-Qj9Kw
metadata:
  title: ''
  description: Manging comments using CMS
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: comments-stock-ui
      title: Comments Stock UI
    - type: basic
      slug: web-comments
      title: Comments
    - type: basic
      slug: comments-stock-ui-1
      title: Comments UI
---
Livelike CMS provides an easy to use front-end to manage your comment boards within an application.

Comment Boards represent topics that can be commented on like blog posts, videos, sports teams, individual matches once they are integrated in client application.\
Comments are posted to boards. A comment can also be a reply to another comment.

As a CMS producer, you can create, edit, delete comment boards, control the nesting depth of comments, post, delete, report, moderate any comment and ban users from posting any comment.

To understand the technical implementation of the SDKs, please visit [https://docs.livelike.com/docs/comment-boards](https://docs.livelike.com/docs/comment-boards)

## Comments section

Producers can access Comments section from the Sidebar, it will display the list of all the Comment Boards in that application.

<Image align="center" src="https://files.readme.io/29c07af-Screenshot_2023-09-04_at_7.22.00_PM.png" />

## Managing Comment Board

### Create a Comment Board

To create a comment board, producer can click on *Create New* button on comment board list page 

<Image align="left" width="800px" src="https://files.readme.io/5cc448c1fdc034a9c49746832fbfb36f0086abc0bc3b9ae38e47b7ac19c508be-Screenshot_2025-04-15_at_12.22.13_PM.png" />

Each Comment Board has following fields:-

**Board Title**: Name of the comment board (It is a required field).

**Custom ID**: Enter custom id for the comment board.

**Description**: Enter description of the comment board.

**Reaction Pack**: Select reaction pack from the dropdown, that you want to associate with the comment board.

**Content filtering**:  To manage the type of comments allowed in a comment board, we provide two levels of\
                                        content filtering. Each level determines how messages are moderated. 

* **1.** `none`: No content filtering, all users can post freely.  
* **2.**`filtered`: Profanity is automatically filtered.

**Allow Comments**: It is set to True by default. Set it to False if you do not want anyone to comment on that board.

**Reply Depth**: Set the reply depth that you want on every comment. This will decide till how many levels, one can reply on a reply.

**Custom Data**: Enter any custom data.

### Edit a Comment Board

To edit a board 

1. Click on **three dots** button of a particular comment board, a popover will appear.

<Image align="center" src="https://files.readme.io/b803207738f98a372e72c06327f4c25ad297fba881558bf8935386a3b5939a37-scc.png" />

2. Click on **Edit Board** button.

<Image align="center" src="https://files.readme.io/2d90adf83d06094314e6bdddae04bb5c7f6f4bf80d2ac5e632f73fc55a7ba345-Screenshot_2025-05-21_at_00.00.38.png" />

3. Update the information that you want and click **Update**.

### Delete a Comment Board

1. Click on **three dots** button of a particular comment board, a popover will appear.
2. Click on **Delete Board**.
3. Click on **Yes, Continue** button to delete a comment board.

## Managing comments in a board

### Post Comment

Apart from the front end, comments can be added from CMS also by a moderator. To make a comment on the comment board, click on the particular comment board, it will display the list of the comments of that particular comment board there click on **Post Comment** button.

![](https://files.readme.io/58fbca8-Screenshot_2023-09-05_at_12.47.55_PM.png)

![](https://files.readme.io/dadf39b-Screenshot_2023-09-05_at_1.03.19_PM.png)

### Reply on a Comment

1. Click on *three dots* button of a particular comment on which you want to reply, a popover will open.

![](https://files.readme.io/f7de9ea-Screenshot_2023-09-05_at_2.13.17_PM.png)

2. Click on *Reply* button to reply on a particular button.

![](https://files.readme.io/8e351ef-Screenshot_2023-09-05_at_2.31.58_PM.png)

3. To view the replies of a comment, click on *\{\{number}} replies*.

![](https://files.readme.io/a8e5fd6-Screenshot_2023-09-05_at_2.47.57_PM.png)

### Delete a Comment

Moderator can delete any comment, while front end users can only delete their own. To delete a comment:

1. Click on **three dots** button of a particular comment, a popover will appear.
2. Click on **Delete Comment**.
3. Click on **Yes, Continue** button to delete a comment. Once a comment is deleted it will be displayed as *This comment was deleted by you!* if you deleted that comment, otherwise it will be displayed as *This comment was deleted by \{\{user\_name}}*.

![](https://files.readme.io/f4f55bb-Screenshot_2023-09-05_at_3.31.20_PM.png)

## Moderating Comments

### Report a Comment

You can see user reported comments under "Reported comments" tab.

You can also report a comment yourself, if you find the comment offensive.

1. Click on **three dots** button of a particular comment, a popover will appear.
2. Click on **Report Comment**.
3. Click on **Yes, Continue** button if you want to report that comment. Once commented, It will appear in a *Reported Comments* tab.

![](https://files.readme.io/1ed24d0-Screenshot_2023-09-05_at_6.29.45_PM.png)

### Delete a Comment Report

Report will be deleted (like it was never reported in the first place). Same user can report the same comment again. This is like Unreporting a comment. Moderator can delete any comment report. To delete a comment report:

1. Click on the **Reported Comments** tab inside comment board.
2. Click on **three dots** button of a particular reported comment, a popover will appear.

![](https://files.readme.io/d757228-Screenshot_2023-09-11_at_4.11.37_PM.png)

3. Click on **Delete Report** button.
4. After confirming the comment will be deleted from reported comments.

### Dismiss a Comment Report

When a comment is marked as reported, then in reported comments it's status will be *Pending* and once moderator dismiss a reported comment then it's status will be changed to *Dismissed* and it will be removed from reported comments list. Report will be dismissed. same user can NOT report the same comment again. To dismiss a reported comment:

1. Click on the **Reported Comments** tab inside comment board.
2. Click on **three dots** of a particular reported comment, a popover will appear.

![](https://files.readme.io/d1e7dea-Screenshot_2023-09-11_at_4.11.37_PM.png)

3. Click on **Dismiss** button.
4. After confirming comment will be marked as *dismissed* and it will be removed from reported comments list in CMS.

### Delete a Reported Comment

Moderator can delete any reported comment, while front end users can only delete their own. To delete a comment:

1. Click on the **Reported Comments** tab inside comment board.
2. Click on **three dots** button of a particular comment, a popover will appear.

![](https://files.readme.io/63a11b8-Screenshot_2023-09-11_at_4.11.37_PM.png)

3. Click on **Delete Comment**.
4. Click on **Yes, Continue** button to delete a comment. Once a comment is deleted it will be displayed as *This comment was deleted by you!* if you deleted that comment, otherwise it will be displayed as *This comment was deleted by \{\{user\_name}}*.

### Ban User from Board

If a you ban any user from particular comment board, then that user cannot comment on that board and also that user cannot reply on any comment of that board. To ban a user from board:

1. Click on **three dots** button of a particular comment made by user to whom you want to ban, a popover will appear.
2. Click on **Ban User from Board**.
3. After confirming that user will be shown on *Banned Users* tab.

![](https://files.readme.io/f330bef-Screenshot_2023-09-05_at_6.41.06_PM.png)

### Globally Ban User

If a you ban any user globally, then that user cannot comment on any of the board and also that user cannot reply on any comment. To ban a user globally:

1. Click on **three dots** button of a particular comment made by user to whom you want to ban, a popover will appear.
2. Click on **Globally Ban User**.
3. After confirming that user will be shown on *Globally Banned Users* tab.

![](https://files.readme.io/247e68b-Screenshot_2023-09-05_at_6.51.15_PM.png)

### Unban User

To unban a banned user globally or from board:

1. Go to the *Globally Banned Users / Banned Users* tab.
2. Click on **three dots** button of a particular user that you want to unban.
3. Click on **Unban User**.

After confirming that user will be unbanned from that board or globally.
