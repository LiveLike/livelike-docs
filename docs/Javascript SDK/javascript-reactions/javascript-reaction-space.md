---
title: Reaction Space
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-user-reaction
      title: User Reaction
---
Reaction space is a resource which lets you add or remove reactions for a given target. It maps your content unique identifier i.e target group Id with reaction pack Id and also helps in achieving a complete isolation of user reactions across different content. This also gives you an opportunity to get all user reactions based on target group Id without needing the reference of reaction space Id.

## Create a Reaction Space

For creating a reaction space, you would need reaction pack Ids where each pack id is a collection of reactions to be used by your users and a target group Id which is a unique identifier of your content referencing collection of items.

```javascript
import { createReactionSpace } from '@livelike/javascript'

createReactionSpace({
    targetGroupId: "target-group-1",
    reactionPackIds: ["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
```

## Update a Reaction Space

You can update name and reaction pack Ids of an existing reaction space.

> 🚧 Reaction space `target_group_id` is readonly
>
> Once a reaction space is created using a given target\_group\_id, it becomes a readonly property of reaction space detail.\
> To update a target group Id, simply create a new reaction space.

```javascript
import { updateReactionSpace } from '@livelike/javascript'

updateReactionSpace({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    reactionPackIds: ["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
```

## Delete a Reaction Space

Use this method to remove Reaction Space for the given `reactionSpaceId` in the object parameter.

```javascript
import { deleteReactionSpace } from '@livelike/javascript'

deleteReactionSpace({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
})
```

## List of Reaction Space

This could be used to get list of reaction spaces in an application.\
It returns a Promise that resolves in paginated list of reaction space objects.

```javascript
import { getReactionSpaces } from '@livelike/javascript'

getReactionSpaces().then(({results}) => console.log(results))
```

## Get Reaction Space Detail

Use this method to get reaction space detail from `reactionSpaceId` or `targetGroupId`

```javascript
import { getReactionSpaceDetail } from '@livelike/javascript'

// get reactio space detail using reactionSpaceId
getReactionSpaceDetail({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionSpace => console.log(reactionSpace))

// get reaction space detail using targetGroupId
getReactionSpaceDetail({
    targetGroupId: "target-group-1",
}).then(reactionSpace => console.log(reactionSpace))
```

## Real time Reaction Space events

Use this method to add event listeners for a given reaction space.\
We have following reaction space events as part of `ReactionSpaceEvent` enum:

1. `ADD_REACTION` -> Event fired when any reaction is added for a given reaction space Id.
2. `REMOVE_REACTION` -> Event fired when any reaction is removed for a given reaction space Id.
3. `UPDATE_REACTION_SPACE` -> Event fired when reaction space is updated with either reaction pack Ids or name of the reaction space.

### Adding listener for  `UPDATE_REACTION_SPACE` event:

```javascript
import { 
  addReactionSpaceEventListener,
  removeReactionSpaceEventListener,      
  ReactionSpaceEvent 
} from '@livelike/javascript'

function onReactionSpaceUpdate(userReaction){
    console.log(userReaction);
}
addReactionSpaceEventListener({
    event: ReactionSpaceEvent.UPDATE_REACTION_SPACE, 
    // or REMOVE_REACTION or ADD_REACTION
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onReactionSpaceUpdate
)

// To remove a event listener
removeReactionSpaceEventListener({
    event: ReactionSpaceEvent.UPDATE_REACTION_SPACE,
    // or REMOVE_REACTION or ADD_REACTION
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onReactionSpaceUpdate
)
```
