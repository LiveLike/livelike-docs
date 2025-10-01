---
title: Chat Moderation
excerpt: Moderating chat inside the CMS
deprecated: false
hidden: false
metadata:
  title: CMS Chat Moderation | Producer Suite | LiveLike Developer Hub
  description: >-
    We have a library of chat moderation tools to allow you to moderate the chat
    inside the CMS. Learn more.
  robots: index
next:
  description: ''
---
## Delete Messages

Chat messages can be removed directly from chats when inside the Producer Suite. Open the message actions menu by clicking the more options icon next to the message, and then select *Delete*.

<Image alt="Open the message actions menu for the message, and select the appropriate Mute option." align="center" src="https://files.readme.io/1a04fb9ee754dfee6f74d9e3499c5f3537c6af9f0b69185c49d3b47eac2a5c9b-image.png">
  Open the message actions menu for the message, and select Delete.
</Image>

## User Reports

Users in chat can report messages, and those reports will show in the Moderation tab for that chat in the Producer Suite. Open the report actions menu, and select *Remove* to delete the reported message, or *Dismiss* the report if it is invalid.

<Image alt="Open the report action menu, and select Dismiss Report or Remove Message." align="center" src="https://files.readme.io/2781cf99d41bcc5191366bf6473c813a79b068f43efae5805a395f0f737a8dbf-image.png">
  Open the report action menu, and select Dismiss Report or Remove Message.
</Image>

## Mute (Chat Room Level)

The Mute feature allows moderators to silence a user in a specific chat room. Once muted, the user cannot send messages in that chat room, though they retain the ability to participate in other chat rooms within the same experience. This action is useful for addressing inappropriate behavior localized to a particular discussion. The mute remains in place until manually removed by a moderator.

## Global Mute

A Global Mute prevents a user from sending messages in any chat room across the entire experience. This option is intended for users who repeatedly violate guidelines or cause widespread disruption. Once applied, the user is restricted from participating in all chat rooms until the mute is removed. Moderation staff can manage such users via the “Muted Users” tab in the CMS.

<Image alt="Open the message actions menu for the message, and select the appropriate Mute option." align="center" src="https://files.readme.io/1a04fb9ee754dfee6f74d9e3499c5f3537c6af9f0b69185c49d3b47eac2a5c9b-image.png">
  Open the message actions menu for the message, and select the appropriate Mute option.
</Image>

## Shadow Mute (Chat Room Level)

A Shadow Mute is used to discreetly mute a user within a single chat room. When shadow-muted, the user continues to see their own messages and believes they are participating normally, but those messages are invisible to all other users. This technique is particularly effective for preventing further disruption while avoiding confrontation or detection. The mute remains effective until manually removed by a moderator.

## Global Shadow Mute

The Global Shadow Mute functionality silences a user across all chat rooms while making their messages appear visible only to themselves. This form of mute is designed to prevent users from realizing they’ve been muted, reducing the likelihood that they’ll attempt to rejoin under a different identity. Global Shadow Mute is especially useful in managing repeat offenders and minimizing disruption across the platform. Moderators can apply or remove this mute directly from the Producer Suite, and the muted user’s status can be tracked in the Muted Users section.

<Image alt="Chat users in muted states." align="center" src="https://files.readme.io/0cd8a19e00055af29c9295f3cb877dd44c48ca449025365e2dc9b3f303993a15-image.png">
  Chat users in muted states.
</Image>

## Automatic Moderation

Chat messages can be automatically filtered based on their contents so that the moderation effort can be reduced. Automatic filters can be set up to work in a couple ways:

* **Keyword-driven**. If a message contains a word from a list of bad words, it will be filtered. The word lists can be customized.
* **AI-driven**. If a message is recognized by an AI model as being objectionable, it will be filtered.

To manage the type of messages allowed in a chat room, we provide three levels of content filtering. Each level determines how messages are moderated and who is allowed to post.  One of these can be selected when creating a chat room through CMS or API.

* **1.** `none`: No content filtering, all users can post freely.  (default)
* **2.**`filtered`: Profanity is automatically filtered. 
* **3.** `producer`: Only producers can post, others can view messages only.

> 📘
>
> Contact support to set up and configure automatic chat moderation.

## Banned Words Customization

Producers can customise banned words for their Application from the Producer Suite.\
Banned Words Customisation can be done by using Manual Add/Delete or by Uploading csv

* **Manual-Customization**\
  Operators can search existing banned word list to filter out words matching the entered string.\
  If the word doesn't exist, operators can add that word.\
  From the filtered list, operators can remove any word.\
  Finally, Operators need to click on Save button to save all the changes made to the banned words list

<Image title="Screenshot 2022-09-19 at 2.07.42 PM.png" alt={1270} align="center" src="https://files.readme.io/33d2203-Screenshot_2022-09-19_at_2.07.42_PM.png">
  Manual-Customization
</Image>

* **CSV-Upload**\
  Operators can download the existing banned word list and made changes to that (add/remove words in the csv)\
  They would need to upload that updated csv on the Producer Suite to reflect the changes in Banned Word List

<Image title="Screenshot 2022-09-19 at 2.07.49 PM.png" alt={1299} align="center" src="https://files.readme.io/d72c564-Screenshot_2022-09-19_at_2.07.49_PM.png">
  CSV-Upload
</Image>