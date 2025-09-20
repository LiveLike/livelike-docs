---
title: Reactions
deprecated: false
hidden: false
metadata:
  robots: index
---
Reactions let fans instantly express how they feel about content — whether it’s cheering for a team, liking a message, or showing support during a big moment.
With LiveLike, **any content that has a unique identifier can support reactions**: chat messages, blog posts, comments, videos, polls, or your own custom items.

<Image align="center" width="300px" src="https://files.readme.io/a165ca3-ReactionsAsAService.png" />

> 📘 Available since:
>
> * **Web SDK** `2.29.0`
> * **Android SDK** `2.54`
> * **iOS SDK** `2.51`

***

## Core Concepts

* **Reaction Pack**
  A collection of reaction types (each with an ID, name, and asset). Packs define the available reactions and can be linked to specific spaces.

* **Reaction Space**
  A namespace that maps your content to reaction packs. Each space contains _targets_ (individual items like chat messages, blog comments, or video moments) that users can react to.

* **User Reaction**
  A single instance of a user reacting to a target inside a reaction space.

***

## Typical Workflow

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

## Exclusive Reaction Packs 🔒

Like stickers, reactions can also be **exclusive**.
Only specific users (based on profile rules) can access them — perfect for **tiered memberships, sponsor rewards, or collectible reaction sets**.

***

## APIs Overview (Developer Reference)

Reactions are exposed via three main APIs:

1. **Reaction Packs API** – create and manage sets of reaction types.
2. **Reaction Spaces API** – map content to packs and handle isolation between content.
3. **User Reactions API** – add, remove, and query user reactions.

> Expand below for SDK examples in **Web, Android, iOS** 👇

<br />

\<details>
&#x20; \<summary>Reaction Packs API\</summary>

&#x20; \<details>
&#x20;   \<summary>#### List Reaction Packs \</summary>

&#x20;   This could be used to get list of reaction pack created through producer suite.

&#x20;   \`\`\`javascript
&#x20;   LiveLike.getReactionPacks().then((\{results}) => console.log(results))
&#x20;   \`\`\`
&#x20;   \`\`\`kotlin
&#x20;     engagementSDK.reaction().getReactionPacks(LiveLikePagination.FIRST,
&#x20;               object : LiveLikeCallback\<List\<ReactionPack>>() \{
&#x20;                   override fun onResponse(result: List\<ReactionPack>?, error: String?) \{
&#x20;                       result?.let \{
&#x20;                           //handle success block}
&#x20;                       }
&#x20;                       error?.let \{
&#x20;                           //handle failure block
&#x20;                       }
&#x20;                   })
&#x20;   \`\`\`
&#x20;   \`\`\`swift
&#x20;   sdk.reaction.getReactionPacks(page: .first) \{ result in
&#x20;   	switch result \{
&#x20;       case .success(let reactionPacks):
&#x20;       	//Success Block
&#x20;       case .failure(let error):
&#x20;       	//Failure Block
&#x20;   	}
&#x20;   }
&#x20;   \`\`\`
&#x20;   \</details>

\<summary>#### Get Reaction Pack Details \</summary>

&#x20;   This could be used to get reaction pack details using reaction pack Id.

&#x20;  &#x20;
LiveLike.getReactionPackDetail(\{
&#x20;   reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionPack => console.log(reactionPack))
1
LiveLike.getReactionPackDetail(\{
2
&#x20;   reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
3
}).then(reactionPack => console.log(reactionPack))
&#x20;   \</details>

\</details>

\<details>
&#x20; \<summary>Reaction Spaces API\</summary>

&#x20; \<details>
&#x20; \<summary>#### Create a Reaction Space\</summary>

For creating a reaction space, you would need reaction pack Ids where each pack id is a collection of reactions to be used by your users and a target group Id which is a unique identifier of your content referencing collection of items.

\`\`\`javascript
LiveLike.createReactionSpace(\{
&#x20;   targetGroupId: "target-group-1",
&#x20;   reactionPackIds: \["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
\`\`\`
\`\`\`kotlin
&#x20;engagementSDK.reaction()
&#x20;           .createReactionSpace(\< name >, \<target-group-id>, \<list of reaction-pack-ids>, object: LiveLikeCallback\<ReactionSpace>()\{
&#x20;           override fun onResponse(result: ReactionSpace?, error: String?) \{
&#x20;               result?.let \{
&#x20;                   //handle success
&#x20;               }
&#x20;               error?.let \{
&#x20;                   //handle failure
&#x20;               }
&#x20;           }
&#x20;           )
\`\`\`
\`\`\`swift
sdk.reaction.createReactionSpace(name: reactionSpaceName, targetGroupID: targetGroupID, reactionPackIDs: \[reactionPackIDs]) \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionSpace):
&#x20;   	//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x9;}
}
\`\`\`
\</details>
\<details>
&#x20; \<summary>#### Update a Reaction Space\</summary>

You can update name and reaction pack Ids of an existing reaction space

\`\`\`javascript
LiveLike.updateReactionSpace(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionPackIds: \["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
\`\`\`
\`\`\`kotlin
engagementSDK.reaction().createReactionSpace(\<reaction-space-id>,\<target-group-id>,\<list of reaction-pack-ids>,object: LiveLikeCallback\<ReactionSpace>()\{
&#x20;  override fun onResponse(result: ReactionSpace?, error: String?) \{ 	  &#x20;
&#x20;  }
)
\`\`\`
\`\`\`swift
sdk.reaction.updateReactionSpace(reactionSpaceID: spaceID, reactionPackIDs: \[reactionPackID]) \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionPackIDList):
&#x20;   	//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x20; }
}
\`\`\`
\</details>

\<details>
&#x20; \<summary>#### Delete a Reaction Space\</summary>

\`\`\`javascript
LiveLike.deleteReactionSpace(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
})
\`\`\`
\`\`\`kotlin
engagementSDK.reaction().deleteReactionSpace(\<reaction-space-id>, object: LiveLikeCallback\<Unit>()\{
&#x20;  override fun onResponse(result: Unit?, error: String?) \{ 	  &#x20;
&#x20;  }
)
\`\`\`
\`\`\`swift
sdk.reaction.deleteReactionSpace(reactionSpaceID: spaceID) \{ result in
&#x9;switch result \{
&#x9;	case .success(let success):
&#x9;		//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x9;}
}
\`\`\`
\</details>

\<details>
&#x20; \<summary>#### List Reaction Spaces\</summary>

This could be used to get list of reaction spaces in an application

\`\`\`javascript
LiveLike.getReactionSpaces().then((\{results}) => console.log(results))
\`\`\`
\`\`\`kotlin
engagementSDK.reaction().getReactionSpaces(\<reaction-space-id>,\<target-group-id>,LiveLikePagination.FIRST,object: LiveLikeCallback\<List\<ReactionSpace>>()\{
&#x20;  override fun onResponse(result: List\<ReactionSpace>?, error: String?) \{ 	  &#x20;
&#x20;  }
)
\`\`\`
\`\`\`swift
sdk.reaction.getReactionSpaces(reactionSpaceID: spaceID, targetGroupID: nil, page: .first, completion: \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionSpaces):
&#x20;   	//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x20; }
})
\`\`\`
\</details>

\<details>
&#x20; \<summary>#### Get Reaction Space details by reaction space ID\</summary>

\`\`\`javascript
LiveLike.getReactionSpaceDetail(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionSpace => console.log(reactionSpace))
\`\`\`
\`\`\`kotlin
engagementSDK.reaction().getReactionSpaceDetails(\<reaction-space-id>,object: LiveLikeCallback\<ReactionSpace>()\{
&#x20;  override fun onResponse(result: ReactionSpace?, error: String?) \{ 	  &#x20;
&#x20;  }
)
\`\`\`
\`\`\`swift
sdk.reaction.getReactionSpaceInfo(reactionSpaceID: spaceID) \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionSpace):
&#x20;   	//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x20; }
}
\`\`\`
\</details>
&#x20;&#x20;
\<details>
&#x20; \<summary>#### Get Reaction Space details by target group ID\</summary>

This could be preferred way which helps you avoid storing reaction space ID for a given target group ID in your system.

\`\`\`javascript
LiveLike.getReactionSpaceDetail(\{
&#x20;   targetGroupId: "target-group-1",
}).then(reactionSpace => console.log(reactionSpace))
\`\`\`
\`\`\`kotlin
engagementSDK.reaction().getReactionSpaces(\<reaction-space-id>,\<target-group-id>,LiveLikePagination.FIRST,object: LiveLikeCallback\<List\<ReactionSpace>>()\{
&#x20;  override fun onResponse(result: List\<ReactionSpace>?, error: String?) \{ 	  &#x20;
&#x20;  }
)
\`\`\`
\`\`\`swift
sdk.reaction.getReactionSpaces(reactionSpaceID: nil, targetGroupID: targetGroupID, page: .first, completion: \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionSpaces):
&#x20;   	//Success block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x9;}
})
\`\`\`

\</details>

\</details>

\<details>
&#x20; \<summary>User Reactions API\</summary>

&#x20; \<details>
&#x20; \<summary>#### Create Reaction Session\</summary>

\`\`\`kotlin
val reactionSession = engagementSDK.createReactionSession(\<reaction-space-id>,\<target-group-id>,errorDelegate)
\`\`\`
\`\`\`swift
reactionSession = self.sdk.reaction.createReactionSession(reactionSpace: reactionSpace)
\`\`\`

\<details>
&#x20; \<summary>#### Add User Reaction\</summary>

This API requires:

1\. reaction space Id
2\. reaction Id of a reaction from a reaction pack
3\. target Id which is unique identifier of the subjected entity being reacted upon

\`\`\`javascript
LiveLike.addUserReaction(\{
&#x20;   targetId: "target-1",
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(reaction => console.log(reaction))
\`\`\`
\`\`\`kotlin
reactionSession.addUserReaction(\<target-id>,\<reaction-id>,\<custom-data>,object:LiveLikeCallback\<UserReaction>()\{
&#x9;override fun onResponse(result: UserReaction?, error: String?) \{
&#x20;  &#x20;
&#x20; }
})
\`\`\`
\`\`\`swift
reactionSession.addUserReaction(targetID: targetID, reactionID: reactionID, customData: nil) \{ result in
&#x9;switch result \{
&#x9;	case .success(let userReaction):
&#x20;   	//Success Block
&#x9;	case .failure(let error):
&#x20;   	// Failure Block
&#x9;}
}
\`\`\`
\</details>
\<details>
&#x20; \<summary>#### List User Reactions by target ID\</summary>

\`\`\`javascript
LiveLike.getUserReactions(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   targetId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(paginatedReactions => console.log(paginatedReactions))
\`\`\`
\`\`\`kotlin
reactionSession.getUserReactions(LiveLikePagination.FIRST,\<target-id>,object:LiveLikeCallback\<List\<UserReaction>>()\{
&#x9;override fun onResponse(result: List\<UserReaction>?, error: String?) \{
&#x20;  &#x20;
&#x20; }
})
\`\`\`
\`\`\`swift
reactionSession.getUserReactions(
&#x20; page: .first,&#x20;
&#x20; reactionSpaceID: spaceID,&#x20;
&#x20; options: GetUserReactionsRequestOptions(reactionID: nil,&#x20;
&#x20;                                         targetID: targetID,&#x20;
&#x20;                                         reactionByID: nil)
) \{ result in
&#x20;  switch result \{
&#x9;	case .success(let userReaction):
&#x20;   	//Success Block
&#x9;	case .failure(let error):
&#x20;   	// Failure Block
&#x9;}
}
\`\`\`
\</details>
\<details>
&#x20; \<summary>#### List User Reactions by reaction type ID\</summary>

\`\`\`javascript
LiveLike.getUserReactions(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionId: "2gddc166-b8c3-4ce9-990e-52352fskj29"
}).then(paginatedReactions => console.log(paginatedReactions))
\`\`\`
\`\`\`kotlin
reactionSession.getUserReactions(LiveLikePagination.FIRST,\<reaction-id>,object:LiveLikeCallback\<List\<UserReaction>>()\{
&#x9;override fun onResponse(result: List\<UserReaction>?, error: String?) \{
&#x20;  &#x20;
&#x20; }
})
\`\`\`
\`\`\`swift
reactionSession.getUserReactions(
&#x20; page: .first,&#x20;
&#x20; reactionSpaceID: spaceID,&#x20;
&#x20; options: GetUserReactionsRequestOptions(reactionID: reactionID,&#x20;
&#x20;                                         targetID: nil,&#x20;
&#x20;                                         reactionByID: nil)
) \{ result in
&#x20;  switch result \{
&#x9;	case .success(let userReaction):
&#x20;   	//Success Block
&#x9;	case .failure(let error):
&#x20;   	// Failure Block
&#x9;}
}
\`\`\`
&#x20;   \</details>

\<details>
&#x20; \<summary>#### Count User Reactions by target IDs\</summary>

This API could be used in case you just need reaction with total count for a given target Id.
You can get total reaction count for a list of target Id where currently total target Ids is limited to 20 for a single API request.

\`\`\`javascript
LiveLike.getUserReactionsCount(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   targetIds: \["0fddc166-b8c3-4ce9-990e-848bde12188b"],
}).then(reaction => console.log(reaction))
\`\`\`
\`\`\`kotlin
reactionSession.getUserReactionsCount(\<list-of-target-ids>,LiveLikePagination.FIRST,object:LiveLikeCallback\<List\<TargetUserReactionCount>>()\{
&#x9;override fun onResponse(result: List\<TargetUserReactionCount>?, error: String?) \{
&#x20;  &#x20;
&#x20; }
})
\`\`\`
\`\`\`swift
reactionSession.getUserReactionsCount(
&#x20; reactionSpaceID: spaceID,&#x20;
&#x20; targetID: \[targetID],&#x20;
&#x20; page: .first
) \{ result in
&#x9;switch result \{
&#x9;	case .success(let reactionCount):
&#x20;   	//Success Block
&#x20;   case .failure(let error):
&#x20;   	//Failure Block
&#x9;}
}
\`\`\`
\</details>

\<details>
&#x20; \<summary>#### Remove User Reaction\</summary>

Remove a user reaction using user reaction Id which is Id of the user reaction object created when a user adds a reaction.

\`\`\`javascript
LiveLike.removeUserReaction(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   userReactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
})
\`\`\`
\`\`\`kotlin
reactionSession.removeUserReaction(\<user-reaction-id>,object:LiveLikeCallback\<Unit>()\{
&#x9;override fun onResponse(result: Unit?, error: String?) \{
&#x20;  &#x20;
&#x20; }
})
\`\`\`
\`\`\`swift
reactionSession.removeUserReaction(userReactionID: reactionID) \{ result in
&#x9;switch result \{
&#x9;	case .success:
&#x20;   	//Success Block
&#x9;	case .failure(let error):
&#x9;		//Failure block
&#x9;}
}
\`\`\`
\</details>
\</details>

***

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
