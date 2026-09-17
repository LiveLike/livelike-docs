---
title: GraphQL v0.16.0
author: Akshay Garg
hidden: true
published_at: '2026-09-17T06:21:15.141Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This release introduces enhancements to the GraphQL API, including Apollo-compatible Apollo Cache Control support, a new UGC Emoji Slider widget, fan flair management, and role and role assignment deletion capabilities for GraphQL Integrators.

### Release Changes

#### Apollo Cache Control

***

* **Cache Control**: Added Apollo-compatible Apollo Cache Control support for generating cache metadata and HTTP `Cache-Control` headers for eligible GraphQL responses.

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