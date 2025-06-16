---
title: User Reaction
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
      slug: javascript-user-profile
      title: User Profile
---
## Add User Reaction

Use this method to add a user reaction.\
It requires: reaction space Id, reaction Id of a reaction from a reaction pack and target Id which is unique identifier of the subjected entity being reacted upon.

```javascript
import { addUserReaction } from '@livelike/javascript'

addUserReaction({
    targetId: "target-1",
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    reactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(reaction => console.log(reaction))
```

## Remove User Reaction

Remove a user reaction using user reaction Id which is Id of the user reaction object created when a user adds a reaction.

```javascript
import { removeUserReaction } from '@livelike/javascript'

removeUserReaction({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    userReactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
})
```

## List of User Reaction using target Id

Use this method to get a paginated list of user reaction based on argument object filters

```javascript
import { getUserReactions } from '@livelike/javascript'

getUserReactions({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    targetId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(paginatedReactions => console.log(paginatedReactions))

getUserReactions({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    reactionId: "2gddc166-b8c3-4ce9-990e-52352fskj29"
}).then(paginatedReactions => console.log(paginatedReactions))
```

## List of target reaction with count

This method could be used in case you just need reaction with total count for a given target Id.\
You can get total reaction count for a list of target Id where currently total target Ids is limited to 20 for a single API request.

```javascript
import { getUserReactionsCount } from '@livelike/javascript'

getUserReactionsCount({
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
    targetIds: ["0fddc166-b8c3-4ce9-990e-848bde12188b"],
}).then(reaction => console.log(reaction))
```

## Real time Add user reaction event

You can attach a listener callback for `ADD_REACTION` event using `addReactionSpaceEventListener` API.\
This listener callback would be called when a user reaction is added. 

```javascript
import { 
  addReactionSpaceEventListener,
  removeReactionSpaceEventListener,      
  ReactionSpaceEvent 
} from '@livelike/javascript'

function onAddUserReaction(userReaction){
    console.log(userReaction);
}
addReactionSpaceEventListener({
    event: ReactionSpaceEvent.ADD_REACTION, 
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onReactionSpaceUpdate
)

// To remove a event listener
removeReactionSpaceEventListener({
    event: ReactionSpaceEvent.ADD_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onAddUserReaction
)
```

## Real time Remove user reaction event

You can attach a listener callback for `REMOVE_REACTION` event using `addReactionSpaceEventListener` API. This listener callback would be called when a user reaction is removed.  

```javascript
import { 
  addReactionSpaceEventListener,
  removeReactionSpaceEventListener,      
  ReactionSpaceEvent 
} from '@livelike/javascript'

function onRemoveUserReaction(userReaction){
    console.log(userReaction);
}

addReactionSpaceEventListener({
    event: ReactionSpaceEvent.REMOVE_REACTION, 
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onRemoveUserReaction
)

// To remove a event listener
removeReactionSpaceEventListener({
    event: ReactionSpaceEvent.REMOVE_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onRemoveUserReaction
)
```
