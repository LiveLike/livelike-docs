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
[block:api-header]
{
  "title": "Create a Reaction Space"
}
[/block]
For creating a reaction space, you would need reaction pack Ids where each pack id is a collection of reactions to be used by your users and a target group Id which is a unique identifier of your content referencing collection of items.
[block:code]
{
  "codes": [
    {
      "code": "import { createReactionSpace } from '@livelike/javascript'\n\ncreateReactionSpace({\n    targetGroupId: \"target-group-1\",\n    reactionPackIds: [\"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\", \"0fddc166-b8c3-4ce9-990e-848bde12188b\"]\n}).then(reactionSpace => console.log(reactionSpace))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Update a Reaction Space"
}
[/block]
You can update name and reaction pack Ids of an existing reaction space.
[block:callout]
{
  "type": "warning",
  "title": "Reaction space `target_group_id` is readonly",
  "body": "Once a reaction space is created using a given target_group_id, it becomes a readonly property of reaction space detail.\nTo update a target group Id, simply create a new reaction space."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import { updateReactionSpace } from '@livelike/javascript'\n\nupdateReactionSpace({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n    reactionPackIds: [\"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\", \"0fddc166-b8c3-4ce9-990e-848bde12188b\"]\n}).then(reactionSpace => console.log(reactionSpace))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Delete a Reaction Space"
}
[/block]
Use this method to remove Reaction Space for the given `reactionSpaceId` in the object parameter.
[block:code]
{
  "codes": [
    {
      "code": "import { deleteReactionSpace } from '@livelike/javascript'\n\ndeleteReactionSpace({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "List of Reaction Space"
}
[/block]
This could be used to get list of reaction spaces in an application.
It returns a Promise that resolves in paginated list of reaction space objects.
[block:code]
{
  "codes": [
    {
      "code": "import { getReactionSpaces } from '@livelike/javascript'\n\ngetReactionSpaces().then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Reaction Space Detail"
}
[/block]
Use this method to get reaction space detail from `reactionSpaceId` or `targetGroupId`
[block:code]
{
  "codes": [
    {
      "code": "import { getReactionSpaceDetail } from '@livelike/javascript'\n\n// get reactio space detail using reactionSpaceId\ngetReactionSpaceDetail({\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\",\n}).then(reactionSpace => console.log(reactionSpace))\n\n// get reaction space detail using targetGroupId\ngetReactionSpaceDetail({\n    targetGroupId: \"target-group-1\",\n}).then(reactionSpace => console.log(reactionSpace))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Real time Reaction Space events"
}
[/block]
Use this method to add event listeners for a given reaction space. 
We have following reaction space events as part of `ReactionSpaceEvent` enum:
1. `ADD_REACTION` -> Event fired when any reaction is added for a given reaction space Id.
2. `REMOVE_REACTION` -> Event fired when any reaction is removed for a given reaction space Id.
3. `UPDATE_REACTION_SPACE` -> Event fired when reaction space is updated with either reaction pack Ids or name of the reaction space.

### Adding listener for  `UPDATE_REACTION_SPACE` event:
[block:code]
{
  "codes": [
    {
      "code": "import { \n  addReactionSpaceEventListener,\n  removeReactionSpaceEventListener,      \n  ReactionSpaceEvent \n} from '@livelike/javascript'\n\nfunction onReactionSpaceUpdate(userReaction){\n    console.log(userReaction);\n}\naddReactionSpaceEventListener({\n    event: ReactionSpaceEvent.UPDATE_REACTION_SPACE, \n    // or REMOVE_REACTION or ADD_REACTION\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonReactionSpaceUpdate\n)\n\n// To remove a event listener\nremoveReactionSpaceEventListener({\n    event: ReactionSpaceEvent.UPDATE_REACTION_SPACE,\n    // or REMOVE_REACTION or ADD_REACTION\n    reactionSpaceId: \"aa7e03fc-01f0-4a98-a2e0-3fed689632d7\"\n},\nonReactionSpaceUpdate\n)",
      "language": "javascript"
    }
  ]
}
[/block]