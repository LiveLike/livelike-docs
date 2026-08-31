---
title: Android SDK 3.0.11
author: Viktor Manev
hidden: false
published_at: '2026-04-08T14:46:33.227Z'
type: added
---
<br />

## What's new

This release adds improvement for comments and reactions.

## Comments

* Added Profile Relations to filtering in Comments.
* New endpoint API

  Count comments in real time across one or multiple Comment Boards, with the option to filter by Profile Relations or include all comments

  ```kotlin
    sdk.commentFeed().getCommentsCount()
  ```

<br />

## Reactions

You can now use reactions in the SDK.

* Added Profile Relations to filtering in User Reactions.
* Fixed specific bug with pagination
* New fields in the User Reaction response ( `target_group_id and url`)