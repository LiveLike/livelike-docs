---
title: Comments
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Comment Feature Functionalities

The `<livelike-comments>` element will insert a fully-functional comment board into your web application, empowering users with features like moderation, reactions, and profanity filtering for engaging discussions.

### a. Comment Board

#### -`boardId` Attribute

To display the complete Comment Feature UI, add the `boardId` attribute to an HTML element, specifying the board's ID. The `boardId` attribute is required and must be a valid board ID. Comment boards can be [created through the API](https://docs.livelike.com/docs/comment-boards)

```html
<script>
LiveLike.init({ clientId })
</script>

<livelike-comments boardId="COMMENT_BOARD_ID"></livelike-comments>
```

Reaction space to can be added to comments using [create reaction space API](https://docs.livelike.com/docs/reactions)

<Embed url="https://codepen.io/harshitachugh/pen/VwqPqmg" title="Comment Board" image="https://shots.codepen.io/username/pen/VwqPqmg-512.jpg?version=1694166085" provider="codepen.io" href="https://codepen.io/harshitachugh/pen/VwqPqmg" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fcodepen.io%252Fharshitachugh%252Fembed%252Fpreview%252FVwqPqmg%253Fdefault-tabs%253Dhtml%25252Cresult%2526height%253D600%2526host%253Dhttps%25253A%25252F%25252Fcodepen.io%2526slug-hash%253DVwqPqmg%26display_name%3DCodePen%26url%3Dhttps%253A%252F%252Fcodepen.io%252Fharshitachugh%252Fpen%252FVwqPqmg%26image%3Dhttps%253A%252F%252Fshots.codepen.io%252Fusername%252Fpen%252FVwqPqmg-512.jpg%253Fversion%253D1694166085%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dcodepen%22%20width%3D%22800%22%20height%3D%22600%22%20scrolling%3D%22no%22%20title%3D%22CodePen%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

#### - Displaying Comments

Users can view comments posted by others. The Comment Board displays comments in a structured and user-friendly format.

#### - Posting Comments

Users can contribute to the discussion by posting comments. They can express their thoughts, ask questions, or share opinions.

#### - Reacting to Comments

Users can react to comments using emojis or custom reaction icons. This feature allows users to express their emotions or agreement with a comment.

<Image align="center" src="https://files.readme.io/5003ed6-Screenshot_2023-09-25_at_6.32.21_PM.png" />

#### - Replying to Comments

`<livelike-comments>` supports threaded discussions, enabling users to reply to specific comments. This fosters more in-depth conversations and keeps discussions organised.

#### - Sorting Comments

Users can sort comments from newest to oldest or oldest to newest. By default ,the comments will be sorted from newest to oldest.

<Image align="center" src="https://files.readme.io/1f0bdd7-Screenshot_2023-09-25_at_6.31.13_PM.png" />

#### - Pagination

Maximum of 20 comments will be visible on first load. User can load more comments by clicking `Load More` button at end of comments list.

<Image align="center" src="https://files.readme.io/8a10105-Screenshot_2023-09-25_at_6.33.00_PM.png" />

### b. Moderation

<Image align="center" width="300px" src="https://files.readme.io/0d95a89-Screenshot_2023-09-11_at_12.40.11_PM.png" />

#### - Reporting Comments

Users can report comments that they find inappropriate or offensive. This feature helps identify and address problematic content.

#### - Blocking Users

Blocking a user prevents them from replying further on your comment. It's a powerful tool to manage troublesome users.

#### - Deleting Comments

<Image align="center" width="300px" src="https://files.readme.io/4f4314d-Screenshot_2023-09-11_at_12.40.01_PM.png" />

Moderators or authorised users can delete comments when necessary.User can also delete self comment. This ensures that inappropriate or harmful comments can be removed promptly.

### c. Profanity Filtering

#### - Enabling Profanity Filtering

You can enable profanity filtering to automatically detect and hide profane language in comments. To enable profanity filtering, you need to pass `contentFilter: 'filtered'`to [createCommentBoard or updateCommentBoard API.](https://docs.livelike.com/docs/comment-boards)

```javascript
LiveLike.createCommentBoard({
  title: 'sd',
  customId:'customId',
  repliesDepth:2,
  allowComments:true,
  description: 'desc',
  customData:'abc',
  contentFilter: 'filtered'
}).then(commentBoard => console.log(commentBoard));
```

When filtering is enabled, comments containing profane/obscene words will be filtered out. 

#### `profaneComment` Attribute

The `profaneComment` attribute allows you to control how profane comments are displayed. You can configure the behaviour of profaneComment either masked with asterisks (e.g., `***`) or according to your custom filter function.

* If you set `profaneComment="mask"`, profane words in the comments will be displayed as asterisks (`***`).

```html
<livelike-comments boardId="COMMENT_BOARD_ID" profaneComment="mask"></livelike-comments>
```

<Image align="center" width="300px" src="https://files.readme.io/7d063b1-image.png" />

#### - Custom Profanity Filter Function

If you have specific requirements for profanity filtering, you can define a custom filter function. This function allows you to implement your filtering logic.

* If you set `profaneComment="custom"`, you can provide your custom logic to handle profane comment using `profaneCommentFilterFunction` attribute.

```html
<livelike-comments boardId="COMMENT_BOARD_ID" profaneComment="custom" profaneCommentFilterFunction={someFunc} >
</livelike-comments>
```

### d. Additional Features

#### - Update/Add Author Image

Users can associate an image with their comment by providing an `authorImageUrl`. This personalizes their comments and adds visual context to their contributions.

<Image align="center" src="https://files.readme.io/85fb2f6-Screenshot_2023-09-11_at_3.14.31_PM.png" />

##### `authorImageUrl` Attribute

You can also specify an author's image URL using the `authorImageUrl` attribute.

```html
<livelike-comments boardId="COMMENT_BOARD_ID" authorImageUrl="URL_TO_AUTHOR_IMAGE"></livelike-comments>
```

`authorImageUrl` can also be passed as a param in the comment board url.

#### - Reaction Packs

`<livelike-comments>` support predefined sets of reactions or emojis that users can choose from when reacting to comments. This can add fun and engagement to your comment system. Reaction space to can be added to comments using [create reaction space API](https://docs.livelike.com/docs/reactions). Assign the comment board Id to `targetGroupId` attribute.

```javascript
LiveLike.createReactionSpace({
  targetGroupId: '603b6329-b682-4af6-86ee-3c10440b6941',
  reactionPackIds: ['0affb9e4-94fc-4fe6-b8bd-70f1d67f26cc'],
}).then((reactionSpace) => console.log(reactionSpace));
```

> Creating a reaction space for a comment board is a one time task that you have to do whenever a comment board is been created

## Customisation

You can customise the appearance and behaviour of the Comment Board to match your application's branding and user experience. This typically involves modifying CSS styles and using event handling to implement custom logic. 

### a. Customise CSS

Styling can be updated using css classes and selectors.

```css
livelike-comments{
  width: 100%;
}

livelike-comment-board-header{
  ...
}
```

Refer [stackblitz](https://stackblitz.com/edit/stackblitz-starters-deacpc.html?file=src%2FApp.tsx) code for customised css.

### b. Customise State

You can customise the behaviour and working of a comment board to suit your requirements. This can be done using controller methods and API methods.

```javascript
const response = await LiveLike.getComments({ordering:"-created_at",since:"2023-08-22T14:30:45.123Z"})
      
const filteredComments = LiveLike.commentController.filterComments({
   blockedProfileIds: new Set(Livelike._$$.blockedProfileIds),
   comments: response.data.results ?? [],
});
const currentState = LiveLike.commentController.getState(commentBoardId);
const newState = { ...currentState, comments: updatedComments };

LiveLike.commentController.setState({
  commentBoardId: commentBoardId,
  newState: newState
});
```

> In the above example getComments is API method for fetching comments and filterComments is a controller method for filtering blocked profile messages.

You can also update the author image url attribute using controller method `updateCommentConfigAction`.

```javascript
LiveLike.commentController.updateCommentConfig({
  commentBoardId: 'c5d2776f-63ea-4bfb-9c3b-ff016a61303b',
  commentBoardConfig: {
    authorImageUrl: 'https://picsum.photos/id/64/200/200',
  },
});
```
