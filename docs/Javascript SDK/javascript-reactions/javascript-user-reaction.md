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
[block:api-header]
{
  "title": "Add User Reaction"
}
[/block]
Use this method to add a user reaction.
It requires: reaction space Id, reaction Id of a reaction from a reaction pack and target Id which is unique identifier of the subjected entity being reacted upon.
[block:code]
{
  "codes": [
    {
      "code": "import { addUserReaction } from '@livelike/javascript'\n\naddUserReaction({\n    targetId: \"target-1\",\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    reactionId: \"0fddc166-b8c3-4ce9-990e-848bde12188b\"\n}).then(reaction => console.log(reaction))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Remove User Reaction"
}
[/block]
Remove a user reaction using user reaction Id which is Id of the user reaction object created when a user adds a reaction.
[block:code]
{
  "codes": [
    {
      "code": "import { removeUserReaction } from '@livelike/javascript'\n\nremoveUserReaction({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    userReactionId: \"0fddc166-b8c3-4ce9-990e-848bde12188b\"\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "List of User Reaction using target Id"
}
[/block]
Use this method to get a paginated list of user reaction based on argument object filters
[block:code]
{
  "codes": [
    {
      "code": "import { getUserReactions } from '@livelike/javascript'\n\ngetUserReactions({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    targetId: \"0fddc166-b8c3-4ce9-990e-848bde12188b\"\n}).then(paginatedReactions => console.log(paginatedReactions))\n\ngetUserReactions({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    reactionId: \"2gddc166-b8c3-4ce9-990e-52352fskj29\"\n}).then(paginatedReactions => console.log(paginatedReactions))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "List of target reaction with count"
}
[/block]
This method could be used in case you just need reaction with total count for a given target Id.
You can get total reaction count for a list of target Id where currently total target Ids is limited to 20 for a single API request.
[block:code]
{
  "codes": [
    {
      "code": "import { getUserReactionsCount } from '@livelike/javascript'\n\ngetUserReactionsCount({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    targetIds: [\"0fddc166-b8c3-4ce9-990e-848bde12188b\"],\n}).then(reaction => console.log(reaction))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Real time Add user reaction event"
}
[/block]
You can attach a listener callback for `ADD_REACTION` event using `addReactionSpaceEventListener` API.
This listener callback would be called when a user reaction is added. 
[block:code]
{
  "codes": [
    {
      "code": "import { \n  addReactionSpaceEventListener,\n  removeReactionSpaceEventListener,      \n  ReactionSpaceEvent \n} from '@livelike/javascript'\n\nfunction onAddUserReaction(userReaction){\n    console.log(userReaction);\n}\naddReactionSpaceEventListener({\n    event: ReactionSpaceEvent.ADD_REACTION, \n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonReactionSpaceUpdate\n)\n\n// To remove a event listener\nremoveReactionSpaceEventListener({\n    event: ReactionSpaceEvent.ADD_REACTION,\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonAddUserReaction\n)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Real time Remove user reaction event"
}
[/block]
You can attach a listener callback for `REMOVE_REACTION` event using `addReactionSpaceEventListener` API. This listener callback would be called when a user reaction is removed.  
[block:code]
{
  "codes": [
    {
      "code": "import { \n  addReactionSpaceEventListener,\n  removeReactionSpaceEventListener,      \n  ReactionSpaceEvent \n} from '@livelike/javascript'\n\nfunction onRemoveUserReaction(userReaction){\n    console.log(userReaction);\n}\n\naddReactionSpaceEventListener({\n    event: ReactionSpaceEvent.REMOVE_REACTION, \n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonRemoveUserReaction\n)\n\n// To remove a event listener\nremoveReactionSpaceEventListener({\n    event: ReactionSpaceEvent.REMOVE_REACTION,\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonRemoveUserReaction\n)",
      "language": "javascript"
    }
  ]
}
[/block]