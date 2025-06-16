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

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fcodepen.io%2Fharshitachugh%2Fembed%2Fpreview%2FVwqPqmg%3Fdefault-tabs%3Dhtml%252Cresult%26height%3D600%26host%3Dhttps%253A%252F%252Fcodepen.io%26slug-hash%3DVwqPqmg&display_name=CodePen&url=https%3A%2F%2Fcodepen.io%2Fharshitachugh%2Fpen%2FVwqPqmg&image=https%3A%2F%2Fshots.codepen.io%2Fusername%2Fpen%2FVwqPqmg-512.jpg%3Fversion%3D1694166085&key=02466f963b9b4bb8845a05b53d3235d7&type=text%2Fhtml&schema=codepen\" width=\"800\" height=\"600\" scrolling=\"no\" title=\"CodePen embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://codepen.io/harshitachugh/pen/VwqPqmg",
  "title": "Comment Board",
  "image": "https://shots.codepen.io/username/pen/VwqPqmg-512.jpg?version=1694166085",
  "provider": "codepen.io",
  "href": "https://codepen.io/harshitachugh/pen/VwqPqmg"
}
[/block]


#### - Displaying Comments

Users can view comments posted by others. The Comment Board displays comments in a structured and user-friendly format.

#### - Posting Comments

Users can contribute to the discussion by posting comments. They can express their thoughts, ask questions, or share opinions.

#### - Reacting to Comments

Users can react to comments using emojis or custom reaction icons. This feature allows users to express their emotions or agreement with a comment.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5003ed6-Screenshot_2023-09-25_at_6.32.21_PM.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


#### - Replying to Comments

`<livelike-comments>` supports threaded discussions, enabling users to reply to specific comments. This fosters more in-depth conversations and keeps discussions organised.

#### - Sorting Comments

Users can sort comments from newest to oldest or oldest to newest. By default ,the comments will be sorted from newest to oldest.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1f0bdd7-Screenshot_2023-09-25_at_6.31.13_PM.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


#### - Pagination

Maximum of 20 comments will be visible on first load. User can load more comments by clicking `Load More` button at end of comments list.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8a10105-Screenshot_2023-09-25_at_6.33.00_PM.png",
        "",
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


### b. Moderation

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


#### - Reporting Comments

Users can report comments that they find inappropriate or offensive. This feature helps identify and address problematic content.

#### - Blocking Users

Blocking a user prevents them from replying further on your comment. It's a powerful tool to manage troublesome users.

#### - Deleting Comments

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

- If you set `profaneComment="mask"`, profane words in the comments will be displayed as asterisks (`***`).

```html
<livelike-comments boardId="COMMENT_BOARD_ID" profaneComment="mask"></livelike-comments>
```

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7d063b1-image.png",
        null,
        ""
      ],
      "align": "center",
      "sizing": "300px"
    }
  ]
}
[/block]


#### - Custom Profanity Filter Function

If you have specific requirements for profanity filtering, you can define a custom filter function. This function allows you to implement your filtering logic.

- If you set `profaneComment="custom"`, you can provide your custom logic to handle profane comment using `profaneCommentFilterFunction` attribute.

```html
<livelike-comments boardId="COMMENT_BOARD_ID" profaneComment="custom" profaneCommentFilterFunction={someFunc} >
</livelike-comments>
```

### d. Additional Features

#### - Update/Add Author Image

Users can associate an image with their comment by providing an `authorImageUrl`. This personalizes their comments and adds visual context to their contributions.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/85fb2f6-Screenshot_2023-09-11_at_3.14.31_PM.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]


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