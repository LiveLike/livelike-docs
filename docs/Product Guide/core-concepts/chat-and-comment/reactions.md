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

## Exclusive Reaction Packs

Exclusive reactions bring a premium layer of expression to chats and comments.
Unlike standard reaction packs, exclusive packs are only available to specific users or groups — letting fans show status, loyalty, or collectibility while giving brands and integrators powerful ways to drive engagement and monetization.

<Callout icon="📘" theme="info">
   Exclusive packs are managed at the profile level. Only profiles that have been granted access will see and use them inside chat or comments. 
</Callout>

**Sample Use Cases**

* In-app purchases for fans who want collectible reactions.
* Team-branded packs available only to official fan groups.
* Collectible reaction packs redeemable through the Rewards Store.
* Gold-tier members unlocking exclusive reactions as part of loyalty benefits.

#### How It Works

* Exclusive reaction packs are marked with an is_exclusive flag.
* Access can be granted, revoked, or automated through purchases, rewards, or tier benefits.
* Fans only see packs they own, keeping the experience personalized and clutter-free.

**APIs – Integrator Experience**

* Grant Access to a Reaction Pack: 
  `POST /api/v1/profiles/{profile_uuid}/reaction-packs/`
  Grants access to an exclusive reaction pack for the specified profile.
  ```
  {
      "reaction_pack_id": "6e654321-abcd-4def-9012-9876543210fe",
      "source": "purchase" 
  }
  ```
* List All Reaction Packs Owned by Profile
  Retrieves a paginated list of all reaction packs currently owned by the specified profile.
  `GET /api/v1/profiles/{profile_uuid}/reaction-packs/`
* Revoke Access to a Reaction Pack
  Revokes the user’s access to a specific reaction pack.
  `DELETE /api/v1/profiles/{profile_uuid}/reaction-packs/{reaction_pack_id}/`
* Reaction Pack Create/Update APIs
  Update existing APIs to enable integrators to control the value of the `is_exclusive` field.
* Usage APIs
  Modify `UserReaction` and `ChatRoomMessageReaction` APIs to ensure users can only use exclusive packs if they have access.

#### To support exclusive ownership of reaction packs by fans, we’ll enhance the data model in two ways:


1. Add is_exclusive Field to ReactionPack Model
   Distinguishes exclusive packs from public ones.
   ```
   class ReactionPack(UUIDModel):
       ...
       is_exclusive = models.BooleanField(default=False)
   ```
2. Add ProfileReactionPack Model
   Tracks which profile owns which reaction pack. Multiple users can own the same exclusive pack (e.g., via purchase, reward, or tier).
   ```
   class ProfileReactionPack(UUIDModel):
       profile = models.ForeignKey(ApplicationProfile, related_name="profile_reaction_packs")
       reaction_pack = models.ForeignKey(ReactionPack, related_name="profile_reaction_packs")
       
       source = models.CharField( // Don't have it in V1
           max_length=31,
           choices=[
               ("purchase", "Purchase"),
               ("reward", "Reward"),
               ("tier", "Tier"),
               ("manual", "Manual"),
           ],
           default="purchase"
       )
       created_at = models.DateTimeField(auto_now_add=True)
       removed_at = models.DateTimeField(null=True, blank=True)

       class Meta:
           constraints = [
               models.UniqueConstraint(
                   fields=("profile", "reaction_pack"),
                   condition=Q(removed_at__isnull=True),
                   name="uniq_profile_reactionpack",
               ),
           ]
   ```

<br />

## APIs Overview (Developer Reference)

Reactions are exposed via three main APIs:

1. **Reaction Packs API** – create and manage sets of reaction types.
2. **Reaction Spaces API** – map content to packs and handle isolation between content.
3. **User Reactions API** – add, remove, and query user reactions.

> Expand below for SDK examples in **Web, Android, iOS** 👇

### 1. Reaction Packs API

<details>
  <summary>List Reaction Packs</summary>

  This could be used to get list of reaction pack created through producer suite.

  ```javascript
  LiveLike.getReactionPacks().then(({results}) => console.log(results))
  ```
  ```kotlin
    engagementSDK.reaction().getReactionPacks(LiveLikePagination.FIRST,
              object : LiveLikeCallback<List<ReactionPack>>() {
                  override fun onResponse(result: List<ReactionPack>?, error: String?) {
                      result?.let {
                          //handle success block}
                      }
                      error?.let {
                          //handle failure block
                      }
                  })
  ```
  ```swift
  sdk.reaction.getReactionPacks(page: .first) { result in
  	switch result {
      case .success(let reactionPacks):
      	//Success Block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>Get Reaction Pack Details</summary>

  This could be used to get reaction pack details using reaction pack Id.

  ```javascript
  LiveLike.getReactionPackDetail({
      reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
  }).then(reactionPack => console.log(reactionPack))
  ```
  ```kotlin
   engagementSDK.reaction()
              .getReactionPackDetails(< reaction -pack - id >, object: LiveLikeCallback<ReactionPack>(){
              override fun onResponse(result: ReactionPack?, error: String?) {
                  result?.let {
                      //handle success
                  }

                  error?.let {
                      //handle error
                  }
              }
              )
  ```
  ```swift
  sdk.reaction.getReactionPackInfo(reactionPackID: packID) { result in
  	switch result {
  		case .success(let reactionPack):
      	//Success block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```
</details>

### 2. Reaction Spaces API

<details>
  <summary>Create a Reaction Space</summary>

  For creating a reaction space, you would need reaction pack Ids where each pack id is a collection of reactions to be used by your users and a target group Id which is a unique identifier of your content referencing collection of items.

  ```javascript
  LiveLike.createReactionSpace({
      targetGroupId: "target-group-1",
      reactionPackIds: ["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
  }).then(reactionSpace => console.log(reactionSpace))
  ```
  ```kotlin
   engagementSDK.reaction()
              .createReactionSpace(< name >, <target-group-id>, <list of reaction-pack-ids>, object: LiveLikeCallback<ReactionSpace>(){
              override fun onResponse(result: ReactionSpace?, error: String?) {
                  result?.let {
                      //handle success
                  }
                  error?.let {
                      //handle failure
                  }
              }
              )
  ```
  ```swift
  sdk.reaction.createReactionSpace(name: reactionSpaceName, targetGroupID: targetGroupID, reactionPackIDs: [reactionPackIDs]) { result in
  	switch result {
  		case .success(let reactionSpace):
      	//Success block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>Update a Reaction Space</summary>

  You can update name and reaction pack Ids of an existing reaction space

  ```javascript
  LiveLike.updateReactionSpace({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      reactionPackIds: ["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
  }).then(reactionSpace => console.log(reactionSpace))
  ```
  ```kotlin
  engagementSDK.reaction().createReactionSpace(<reaction-space-id>,<target-group-id>,<list of reaction-pack-ids>,object: LiveLikeCallback<ReactionSpace>(){
     override fun onResponse(result: ReactionSpace?, error: String?) { 	   
     }
  )
  ```
  ```swift
  sdk.reaction.updateReactionSpace(reactionSpaceID: spaceID, reactionPackIDs: [reactionPackID]) { result in
  	switch result {
  		case .success(let reactionPackIDList):
      	//Success block
      case .failure(let error):
      	//Failure Block
    }
  }
  ```
</details>

<details>
  <summary>Delete a Reaction Space</summary>

  ```javascript
  LiveLike.deleteReactionSpace({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
  })
  ```
  ```kotlin
  engagementSDK.reaction().deleteReactionSpace(<reaction-space-id>, object: LiveLikeCallback<Unit>(){
     override fun onResponse(result: Unit?, error: String?) { 	   
     }
  )
  ```
  ```swift
  sdk.reaction.deleteReactionSpace(reactionSpaceID: spaceID) { result in
  	switch result {
  		case .success(let success):
  			//Success block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>List Reaction Spaces</summary>

  This could be used to get list of reaction spaces in an application

  ```javascript
  LiveLike.getReactionSpaces().then(({results}) => console.log(results))
  ```
  ```kotlin
  engagementSDK.reaction().getReactionSpaces(<reaction-space-id>,<target-group-id>,LiveLikePagination.FIRST,object: LiveLikeCallback<List<ReactionSpace>>(){
     override fun onResponse(result: List<ReactionSpace>?, error: String?) { 	   
     }
  )
  ```
  ```swift
  sdk.reaction.getReactionSpaces(reactionSpaceID: spaceID, targetGroupID: nil, page: .first, completion: { result in
  	switch result {
  		case .success(let reactionSpaces):
      	//Success block
      case .failure(let error):
      	//Failure Block
    }
  })
  ```
</details>

<details>
  <summary>Get Reaction Space details by reaction space ID</summary>

  ```javascript
  LiveLike.getReactionSpaceDetail({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
  }).then(reactionSpace => console.log(reactionSpace))
  ```
  ```kotlin
  engagementSDK.reaction().getReactionSpaceDetails(<reaction-space-id>,object: LiveLikeCallback<ReactionSpace>(){
     override fun onResponse(result: ReactionSpace?, error: String?) { 	   
     }
  )
  ```
  ```swift
  sdk.reaction.getReactionSpaceInfo(reactionSpaceID: spaceID) { result in
  	switch result {
  		case .success(let reactionSpace):
      	//Success block
      case .failure(let error):
      	//Failure Block
    }
  }
  ```
</details>

<details>
  <summary>Get Reaction Space details by target group ID </summary>

  This could be preferred way which helps you avoid storing reaction space ID for a given target group ID in your system.

  ```javascript
  LiveLike.getReactionSpaceDetail({
      targetGroupId: "target-group-1",
  }).then(reactionSpace => console.log(reactionSpace))
  ```
  ```kotlin
  engagementSDK.reaction().getReactionSpaces(<reaction-space-id>,<target-group-id>,LiveLikePagination.FIRST,object: LiveLikeCallback<List<ReactionSpace>>(){
     override fun onResponse(result: List<ReactionSpace>?, error: String?) { 	   
     }
  )
  ```
  ```swift
  sdk.reaction.getReactionSpaces(reactionSpaceID: nil, targetGroupID: targetGroupID, page: .first, completion: { result in
  	switch result {
  		case .success(let reactionSpaces):
      	//Success block
      case .failure(let error):
      	//Failure Block
  	}
  })
  ```
</details>

### 3. User Reactions API

<details>
  <summary>Create Reaction Session</summary>

  ```kotlin
  val reactionSession = engagementSDK.createReactionSession(<reaction-space-id>,<target-group-id>,errorDelegate)
  ```
  ```swift
  reactionSession = self.sdk.reaction.createReactionSession(reactionSpace: reactionSpace)
  ```
</details>

<details>
  <summary>Add User Reaction</summary>

  This API requires:

  1. reaction space Id
  2. reaction Id of a reaction from a reaction pack
  3. target Id which is unique identifier of the subjected entity being reacted upon

  ```javascript
  LiveLike.addUserReaction({
      targetId: "target-1",
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      reactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
  }).then(reaction => console.log(reaction))
  ```
  ```kotlin
  reactionSession.addUserReaction(<target-id>,<reaction-id>,<custom-data>,object:LiveLikeCallback<UserReaction>(){
  	override fun onResponse(result: UserReaction?, error: String?) {
      
    }
  })
  ```
  ```swift
  reactionSession.addUserReaction(targetID: targetID, reactionID: reactionID, customData: nil) { result in
  	switch result {
  		case .success(let userReaction):
      	//Success Block
  		case .failure(let error):
      	// Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>List User Reactions by target ID</summary>

  ```javascript
  LiveLike.getUserReactions({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      targetId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
  }).then(paginatedReactions => console.log(paginatedReactions))
  ```
  ```kotlin
  reactionSession.getUserReactions(LiveLikePagination.FIRST,<target-id>,object:LiveLikeCallback<List<UserReaction>>(){
  	override fun onResponse(result: List<UserReaction>?, error: String?) {
      
    }
  })
  ```
  ```swift
  reactionSession.getUserReactions(
    page: .first, 
    reactionSpaceID: spaceID, 
    options: GetUserReactionsRequestOptions(reactionID: nil, 
                                            targetID: targetID, 
                                            reactionByID: nil)
  ) { result in
     switch result {
  		case .success(let userReaction):
      	//Success Block
  		case .failure(let error):
      	// Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>List User Reactions by reaction type ID</summary>

  #### List User Reactions by reaction type ID

  ```javascript
  LiveLike.getUserReactions({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      reactionId: "2gddc166-b8c3-4ce9-990e-52352fskj29"
  }).then(paginatedReactions => console.log(paginatedReactions))
  ```
  ```kotlin
  reactionSession.getUserReactions(LiveLikePagination.FIRST,<reaction-id>,object:LiveLikeCallback<List<UserReaction>>(){
  	override fun onResponse(result: List<UserReaction>?, error: String?) {
      
    }
  })
  ```
  ```swift
  reactionSession.getUserReactions(
    page: .first, 
    reactionSpaceID: spaceID, 
    options: GetUserReactionsRequestOptions(reactionID: reactionID, 
                                            targetID: nil, 
                                            reactionByID: nil)
  ) { result in
     switch result {
  		case .success(let userReaction):
      	//Success Block
  		case .failure(let error):
      	// Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>Count User Reactions by target IDs</summary>

  This API could be used in case you just need reaction with total count for a given target Id.
  You can get total reaction count for a list of target Id where currently total target Ids is limited to 20 for a single API request.

  ```javascript
  LiveLike.getUserReactionsCount({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      targetIds: ["0fddc166-b8c3-4ce9-990e-848bde12188b"],
  }).then(reaction => console.log(reaction))
  ```
  ```kotlin
  reactionSession.getUserReactionsCount(<list-of-target-ids>,LiveLikePagination.FIRST,object:LiveLikeCallback<List<TargetUserReactionCount>>(){
  	override fun onResponse(result: List<TargetUserReactionCount>?, error: String?) {
      
    }
  })
  ```
  ```swift
  reactionSession.getUserReactionsCount(
    reactionSpaceID: spaceID, 
    targetID: [targetID], 
    page: .first
  ) { result in
  	switch result {
  		case .success(let reactionCount):
      	//Success Block
      case .failure(let error):
      	//Failure Block
  	}
  }
  ```
</details>

<details>
  <summary>Remove User Reaction</summary>

  Remove a user reaction using user reaction Id which is Id of the user reaction object created when a user adds a reaction.

  ```javascript
  LiveLike.removeUserReaction({
      reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
      userReactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
  })
  ```
  ```kotlin
  reactionSession.removeUserReaction(<user-reaction-id>,object:LiveLikeCallback<Unit>(){
  	override fun onResponse(result: Unit?, error: String?) {
      
    }
  })
  ```
  ```swift
  reactionSession.removeUserReaction(userReactionID: reactionID) { result in
  	switch result {
  		case .success:
      	//Success Block
  		case .failure(let error):
  			//Failure block
  	}
  }
  ```
</details>

## Real-Time Events

For real time updates of user reactions, please conform to **ReactionSessionDelegate**

Realtime notifications for addition and removal of user reactions.

```swift
func reactionSession(_ reactionSession: ReactionSession, didAddReaction reaction: UserReaction)

func reactionSession(_ reactionSession: ReactionSession, didRemoveReaction reaction: UserReaction)
```

### Real Time Reaction Space events

For real time updates of reactions, please conform to **ReactionClientDelegate**

This event is triggered whenever a reaction space is updated with its name or reaction pack ids. You may need to use this event to update your reaction list based on updated reaction pack Ids.

```swift
func reactionClient(_ reactionClient: ReactionClient, didUpdateReactionSpace newReactionSpace: ReactionSpace)
```

***

In short: **Reactions make every piece of content more interactive, expressive, and fun.**
They’re lightweight for users, flexible for integrators, and powerful for PMs to drive engagement and monetization.
