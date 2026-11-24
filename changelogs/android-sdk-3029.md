---
title: Android SDK  3.0.29
author: Viktor Manev
hidden: true
published_at: '2026-11-24T16:59:13.839Z'
---
#### Whats new

- Fetch reaction counts across multiple spaces using reactionSpaceIds, with optional targetGroupId filtering.
- Count results now include the space and group IDs, making targets easier to identify.
- The single reactionSpaceId is deprecated but still supported. When both inputs are provided, IDs are combined without duplicates.
- Requests now require 1–100 target IDs and support up to 100 unique reaction spaces.
- Updating: Use named arguments when creating GetUserReactionsCountRequest, as the parameter order has changed.<br /><br />more info:<br />[https://docs.livelike.com/reference/get-user-reaction-count](https://docs.livelike.com/reference/get-user-reaction-count "https://docs.livelike.com/reference/get-user-reaction-count")

  <br />

```kotlin Sample
sdk.reaction().getUserReactionsCount(request = GetUserReactionsCountRequest(
targetIds = listOf(myReactionTargetIds), 
reactionSpaceIds = listOf(myReactionSpaceId))
) { result, error -> println(result)       }
```