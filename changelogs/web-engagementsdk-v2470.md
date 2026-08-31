---
title: Web engagementsdk v2.47.0
author: ReadMe API
hidden: false
published_at: '2023-08-10T10:53:54.131Z'
---
### What's New:

* added `authorImageUrl` arg prop to `addComment` and `addCommentReply` API.
* added `contentFilter` arg prop to `createCommentBoard` and `updateCommentBoard` API.
* added `livelike-reaction` component that would enable showing user reactions and performing add/remove user reaction actions.
* added reactions in `livelike-comments` where if a reaction space is created for a comment board, user could add/remove reaction on every comment/reply.
* added moderation capability to `livelike-comments` where user could block comment author, report comments and delete self comments.
* every moderation action shows a info/error banner for `livelike-comments`.
* added showing spinner when loading replies for `livelike-comments`.
* added `commentController`, `bannerController`, `userReactionController`, `reactionSpaceController` and `reactionPackController` to extend/customise default `livelike-comments` behaviour.

### Fixes:

* fix placeholder text for `livelike-comments` composer which now supports localization.
* fix minor UI styles for `livelike-comments`.