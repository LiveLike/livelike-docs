---
title: GraphQL v0.16.0
author: Akshay Garg
hidden: false
metadata:
  robots: noindex
published_at: '2026-09-17T06:21:15.141Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This release introduces widgets Emoji Slider, Flair, and update on RBAC. Support for Apollo Cache Control.

### Release Changes

</br>

#### Apollo-compatible cache control for GraphQL Yoga

***

Support for Apollo Server's cache-control behavior to GraphQL Yoga.

#### Slider

***

* **emojiSlider**: Fetch an Emoji Slider widget by ID.
* **createEmojiSlider**: Create an Emoji Slider widget.
* **createEmojiSliderVote**: Vote on an Emoji Slider widget.
* **updateEmojiSliderVote**: Update a vote on an Emoji Slider widget.
* **publishEmojiSlider**: Publish an Emoji Slider widget.
* **deleteEmojiSlider**: Delete an Emoji Slider widget.

#### Flair

***

* **flair**: Fetch a flair by ID.
* **flairs**: Get all flairs based on provided filters.
* **flairScope**: Fetch a flair scope by ID.
* **flairScopes**: Get all flair scopes based on provided filters.
* **flairAssignment**: Fetch a flair assignment by ID.
* **flairAssignments**: Get all flair assignments based on provided filters.
* **createFlair**: Create a new flair.
* **createFlairAssignment**: Create a new flair assignment.
* **updateFlair**: Update an existing flair.
* **deleteFlair**: Delete an existing flair.
* **deleteFlairAssignment**: Delete an existing flair assignment.

#### RBAC

***

* **deleteRole**: Delete an existing Role.
* **deleteRoleAssignment**: Delete an existing Role Assignment.