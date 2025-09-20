---
title: Reactions
deprecated: false
hidden: false
metadata:
  robots: index
---
Reactions let fans instantly express how they feel about content — whether it’s cheering for a team, liking a message, or showing support during a big moment.
With LiveLike, any content that has a unique identifier can support reaction: chat messages, blog posts, comments, videos, polls, or your own custom items.

<Image align="center" width="300px" src="https://files.readme.io/a165ca3-ReactionsAsAService.png" />

> 📘 Available since:
>
> * **Web SDK** `2.29.0`
> * **Android SDK** `2.54`
> * **iOS SDK** `2.51`

***

### Core Concepts

* **Reaction Pack**
  A collection of reaction types (each with an ID, name, and asset). Packs define the available reactions and can be linked to specific spaces.

* **Reaction Space**
  A namespace that maps your content to reaction packs. Each space contains _targets_ (individual items like chat messages, blog comments, or video moments) that users can react to.

* **User Reaction**
  A single instance of a user reacting to a target inside a reaction space.

***

### Typical Workflow

1. **Create a Reaction Pack** – via Producer Suite or API.
2. **Create Reaction Spaces** – one per content unit (e.g. a chat room, video, blog post), linked with the right packs.
3. **Add User Reactions** – users select a reaction from a pack and attach it to a specific target (e.g. a message ID or video moment).

👉 Example:

* In video apps, the target group ID = video ID, targets = video moments.
* In chat apps, the target group ID = chat room ID, targets = message IDs.

***

## Why Use Reactions?

* **Instant Engagement** – give users lightweight ways to interact beyond chat.
* **Content-Specific Customization** – holiday themes, team-specific packs, sponsor-driven packs.
* **Exclusive Access** – reward loyalty tiers or premium members with special reaction packs.
* **Real-Time Feedback** – surface trends, bursts of excitement, and engagement insights.

***

## Exclusive Reaction Packs

Like stickers, reactions can also be exclusive.
Only specific users (based on profile rules) can access them — perfect for tiered memberships, sponsor rewards, or collectible reaction sets.

***

## APIs Overview (Developer Reference)

Reactions are exposed via three main APIs:

1. **Reaction Packs API** – create and manage sets of reaction types.
2. **Reaction Spaces API** – map content to packs and handle isolation between content.
3. **User Reactions API** – add, remove, and query user reactions.

> Expand below for SDK examples in **Web, Android, iOS** 👇

\<details>
&#x20; \<summary>📦 Reaction Packs API\</summary>

&#x20; Reaction Packs define the \*\*types of reactions\*\* (like 👍, ❤️, 🔥) available to users. &#x20;
&#x20; Use these APIs to list packs, fetch details, and configure them in your apps.

&#x20; \#### List Reaction Packs

&#x20; \`\`\`javascript
&#x20; LiveLike.getReactionPacks().then((\{results}) => console.log(results))
engagementSDK.reaction().getReactionPacks(LiveLikePagination.FIRST,
&#x20;   object : LiveLikeCallback\<List\<ReactionPack>>() \{
&#x20;       override fun onResponse(result: List\<ReactionPack>?, error: String?) \{
&#x20;           // handle success or error
&#x20;       }
&#x20;   })
sdk.reaction.getReactionPacks(page: .first) \{ result in
&#x20; switch result \{
&#x20;   case .success(let reactionPacks):&#x20;
&#x20;     // Success Block
&#x20;   case .failure(let error):&#x20;
&#x20;     // Failure Block
&#x20; }
}
Get Reaction Pack Details
LiveLike.getReactionPackDetail(\{
&#x20;   reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionPack => console.log(reactionPack))
engagementSDK.reaction()
&#x20;   .getReactionPackDetails(\<reaction-pack-id>, object: LiveLikeCallback\<ReactionPack>() \{
&#x20;       override fun onResponse(result: ReactionPack?, error: String?) \{
&#x20;           // handle success or error
&#x20;       }
&#x20;   })
sdk.reaction.getReactionPackInfo(reactionPackID: packID) \{ result in
&#x20; switch result \{
&#x20;   case .success(let reactionPack):&#x20;
&#x20;     // Success Block
&#x20;   case .failure(let error):&#x20;
&#x20;     // Failure Block
&#x20; }
}
\</details>
\<details> \<summary>🌌 Reaction Spaces API\</summary>
A Reaction Space links your content (chat rooms, videos, blog posts) with reaction packs.
Use these APIs to create, update, or delete spaces and listen for real-time updates.
Create a Reaction Space
LiveLike.createReactionSpace(\{
&#x20;   targetGroupId: "target-group-1",
&#x20;   reactionPackIds: \["pack-id-1", "pack-id-2"]
}).then(reactionSpace => console.log(reactionSpace))
engagementSDK.reaction().createReactionSpace(
&#x20;   \<name>, \<target-group-id>, \<list-of-reaction-pack-ids>,&#x20;
&#x20;   object: LiveLikeCallback\<ReactionSpace>() \{
&#x20;       override fun onResponse(result: ReactionSpace?, error: String?) \{
&#x20;           // handle success or error
&#x20;       }
&#x20;   })
sdk.reaction.createReactionSpace(
&#x20; name: reactionSpaceName,&#x20;
&#x20; targetGroupID: targetGroupID,&#x20;
&#x20; reactionPackIDs: \[reactionPackIDs]
) \{ result in
&#x20; switch result \{
&#x20;   case .success(let reactionSpace):&#x20;
&#x20;     // Success Block
&#x20;   case .failure(let error):&#x20;
&#x20;     // Failure Block
&#x20; }
}
Update a Reaction Space
LiveLike.updateReactionSpace(\{
&#x20;   reactionSpaceId: "space-id",
&#x20;   reactionPackIds: \["pack-id-1", "pack-id-2"]
}).then(reactionSpace => console.log(reactionSpace))
Delete a Reaction Space
LiveLike.deleteReactionSpace(\{ reactionSpaceId: "space-id" })
List Reaction Spaces
LiveLike.getReactionSpaces().then((\{results}) => console.log(results))
Get Reaction Space Details (by ID or Target Group ID)
LiveLike.getReactionSpaceDetail(\{ reactionSpaceId: "space-id" })
LiveLike.getReactionSpaceDetail(\{ targetGroupId: "target-group-1" })
🔔 Real-Time Reaction Space Events
Subscribe to reaction activity:
Add Reaction
Remove Reaction
Update Reaction Space
function onAddUserReaction(userReaction) \{
&#x20;   console.log(userReaction);
}
LiveLike.addReactionSpaceEventListener(\{
&#x20;   event: LiveLike.ReactionSpaceEvent.ADD\_REACTION,
&#x20;   reactionSpaceId: "space-id"
}, onAddUserReaction)
\</details>
\<details> \<summary>🙋 User Reactions API\</summary>
User Reactions represent a single fan’s reaction to a target (e.g., chat message, video moment).
Use these APIs to add, list, count, or remove reactions.
Create Reaction Session
val reactionSession = engagementSDK.createReactionSession(\<space-id>, \<target-group-id>, errorDelegate)
reactionSession = sdk.reaction.createReactionSession(reactionSpace: reactionSpace)
Add User Reaction
LiveLike.addUserReaction(\{
&#x20;   targetId: "target-1",
&#x20;   reactionSpaceId: "space-id",
&#x20;   reactionId: "reaction-id"
}).then(reaction => console.log(reaction))
List User Reactions
By Target ID
By Reaction Type ID
LiveLike.getUserReactions(\{
&#x20;   reactionSpaceId: "space-id",
&#x20;   targetId: "target-1"
}).then(console.log)
Count Reactions (per Target)
LiveLike.getUserReactionsCount(\{
&#x20;   reactionSpaceId: "space-id",
&#x20;   targetIds: \["target-1"]
}).then(console.log)
Remove User Reaction
LiveLike.removeUserReaction(\{
&#x20;   reactionSpaceId: "space-id",
&#x20;   userReactionId: "reaction-id"
})
\</details> \`\`\`

***

## Real-Time Events

Developers can subscribe to **real-time events** such as:

* `ADD_REACTION` – when a user reacts.
* `REMOVE_REACTION` – when a user removes their reaction.
* `UPDATE_REACTION_SPACE` – when packs linked to a space change.

SDK delegates and listeners are available across **Web, Android, and iOS**.

***

## Example Use Cases

* ❤️ React to specific **chat messages** in a live chat.
* 🎬 Show excitement during **video highlights** or time-coded moments.
* 📝 Add reactions to **comments on blog posts**.
* 🎉 Provide **exclusive sponsor-branded reactions** for premium fans.

***

👉 In short: **Reactions make every piece of content more interactive, expressive, and fun.**
They’re lightweight for users, flexible for integrators, and powerful for PMs to drive engagement and monetization.
