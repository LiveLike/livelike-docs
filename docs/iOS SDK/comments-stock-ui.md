---
title: Comments Stock UI
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
The Stock UI for Comments as a Service is a plug-and-play kind of UI that enables you to integrate Comments and many of its features into your application very quickly and easily.

This is a guide to help integrate Comments Stock UI and customize your application's experience.

## Initialization

The `CommentsViewController` will insert a fully functional comment board into your application, empowering users with features like moderation, reactions, and profanity filtering for engaging discussions.

It can be initialized using the init function which expects a `CommentBoard`, `CommentClient`, `commentBoardID`, `profileID`, `UserClient`,`ReactionClient` (optional) and `reactionSpace` (optional) as shown in the code example below.

Comment Boards can be created using  [Comment Board APIs](https://docs.livelike.com/docs/comment-boards)

Reaction Spaces can be created using [Reaction Space APIs](https://docs.livelike.com/docs/reactions)

```swift
let vc = CommentsViewController(
	commentBoard: commentBoard,
  commentClient: commentClient,
  reaction: self.sdk.reaction, 
  reactionSpace: self.reactionSpace,
  profileID: profileID,
  userClient: self.userClient
)

vc.modalPresentationStyle = .fullScreen
self.present(vc, animated: true)
```

### - Displaying Comments

Users can view comments posted by others. The Comment Board displays comments in a structured and user-friendly format.

### - Posting Comments

Users can contribute to the discussion by posting comments. They can express their thoughts, ask questions, or share opinions.

### - Reacting to Comments

Users can react to comments using emojis or custom reaction icons. This feature allows users to express their emotions or agreement with a comment.

### - Replying to Comments

Stock UI for Comments supports threaded discussions, enabling users to reply to specific comments. This fosters more in-depth conversations and keeps discussions organised.

## Moderation

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0d95a89-Screenshot_2023-09-11_at_12.40.11_PM.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "300px"
    }
  ]
}
[/block]

### - Reporting Comments

Users can report comments that they find inappropriate or offensive. This feature helps identify and address problematic content.

### - Blocking Users

Blocking a user prevents them from replying further on your comment. It's a powerful tool to manage troublesome users.

### - Deleting Comments

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4f4314d-Screenshot_2023-09-11_at_12.40.01_PM.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "300px"
    }
  ]
}
[/block]

Moderators or authorized users can delete comments when necessary. Users can also delete their own comments. This ensures that inappropriate or harmful comments can be removed promptly.

### - Profanity Filtering

You can enable profanity filtering for Comment Boards using the LiveLike CMS which then allows the text of comments to be filtered based on the profanity filters configuration in the CMS.

## Additional Features

### - Add Author Image

Users can associate an image with their comment by providing an `authorImageUrl` as a part of the `Comment` object. This personalizes their comments and adds visual context to their contributions.

### - Reaction Packs

Stock UI for Comments support predefined sets of reactions or emojis that users can choose from when reacting to comments. This can add fun and engagement to your comments service. Reaction space can be added to comments using [create reaction space API](https://docs.livelike.com/docs/reactions). Assign the comment board ID to `targetGroupId` attribute.

```swift swift
self.sdk.reaction.createReactionSpace(
  name: nil, 
  targetGroupID: commentBoardID, 
  reactionPackIDs: [reactPack.id]) { result in
		switch result {
      case .failure(let error):
      	print("Reaction Space Error: \(error)")
      case .success(let reactionSpace):
       //Use reaction space for comments UI initialization
	}
}
```

> 📘 Creating a reaction space for a comment board is a one time task that you have to do whenever a comment board is been created

## Customization

You can customize the appearance and behavior of the Comment Stock UI to match your application's branding and user experience. This typically involves modifying values in the `Theme` 

### Customize Theme

An example snippet of how the `Theme` can be used to customize the appearance of the Stock UI is shown below.

```swift
private func getCustomTheme() -> Theme {
        let customTheme = Theme()
        customTheme.commentTextLabelColor = UIColor(red: 0, green: 0, blue: 0, alpha: 1)
        customTheme.commentAuthorLabelTextColor = UIColor(red: 0, green: 0, blue: 0, alpha: 1)
        customTheme.commentTimestampLabelTextColor = .darkGray
        customTheme.commentBoardBackgroundColor = UIColor.white
        customTheme.commentViewBackgroundColor = UIColor(red: 0.94, green: 0.96, blue: 0.98, alpha: 1)
        customTheme.commentsFooterViewAlignment = .horizontal
        customTheme.commentRepliesListButtonBackgroundColor = .clear
        customTheme.commentRepliesListButtonTintColor = UIColor(red: 0.19, green: 0.4, blue: 0.96, alpha: 1)
        if let imageIcon = UIImage(named: "reactionImage") {
            customTheme.commentReactionsButtonIconImage = imageIcon.withRenderingMode(.automatic)
        }
        customTheme.commentReactionsButtonTintColor = UIColor(red: 0.19, green: 0.4, blue: 0.96, alpha: 1)
        return customTheme
}
```