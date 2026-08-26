---
title: Reactions
excerpt: Reactions as a service allows users to add reactions to any content
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Use the Reactions service to add user reactions to your content. Anything that can be referenced by a unique identifier is eligible for reactions, so everything ranging from built-in LiveLike components to your own custom content can support user reactions.


<Image src="https://files.readme.io/a165ca3-ReactionsAsAService.png" align="center" width="300px" />


<Callout icon="📘" theme="info">
  ### Available since:

  **Web SDK** `2.29.0`

  **Android SDK** `2.54`

  **iOS SDK** `2.51`
</Callout>

## Reactions Basics

The reactions service consists of a few components.

- A **Reaction Pack** defines a set of reaction types. Each pack can have many reaction types inside of it, and each type has an ID, name, and image asset. Once a pack is created it can be associated with spaces in order to make its reaction types available inside those spaces.
- A **Reaction Space** acts as namespace and mapping for content. Targets within each space represent individual units inside the space that can be reacted to. Packs can be linked with spaces to control which reactions are available to use inside those spaces. Reaction spaces are usually mapped one-to-one with content like chat rooms, comment boards, blog posts, videos, and so on.
- A **User Reaction** is an instance of a user adding their reaction to some target within the space.

## Typical Reactions Workflow

A typical reaction workflow involves setting up reaction packs, mapping those packs to your content through reaction spaces, and then creating user reactions inside the reaction spaces.

1. Creating a Reaction Pack, either through the Producer Suite or via the API.
2. Creating Reaction Spaces for each unit of content that users will be reacting to. Each space should specify the reaction packs that will be available inside the space, and the unique ID of the content. The content's unique ID is specified in the **Target Group ID** field on the space.
   1. In a video application the target group ID could be a "Video ID" which has a collection of video moments.
   2. In a blog post application the target group ID could be a "Blog post Id" which has a collection of blog post comments.
   3. In a chat application the target group ID could be a "Chat room Id" which has a collection of chat messages
3. Adding user reactions. Each user reaction requires the space ID, the reaction type ID, and the target ID of the thing being reacted to. The target ID is not necessarily the same as the target group ID. For example, in a chat use case, the chat room ID would be the target group ID, and individual message IDs would be target IDs.

## Video Reactions Use Case

Imagine you want to allow your users to react to important moments in videos. Each video would have a reaction space associated with it, and moments inside the video would be represented by targets within the video's reaction space. Each moment would need some kind of unique identifier, so timecodes, chapters, or any other ID from your system would work as long as it's unique inside the reaction space.

## Exclusive Reaction Packs

Reactions let fans instantly express how they feel about content, whether it’s cheering for a team, liking a message, or showing support during a big moment.
With LiveLike, **any content that has a unique identifier can support reactions**: chat messages, blog posts, comments, videos, polls, or your own custom items.

<Callout icon="📘" theme="info">
  Exclusive packs are managed at the profile level. Only profiles that have been granted access will see and use them inside chat or comments.
</Callout>

**Sample Use Cases**

- In-app purchases for fans who want collectible reactions.
- Team-branded packs available only to official fan groups.
- Collectible reaction packs redeemable through the Rewards Store.
- Gold-tier members unlocking exclusive reactions as part of loyalty benefits.

#### How It Works

- Access can be granted, revoked, or automated through purchases, rewards, or membership tiers.
- Fans only see the packs they own, keeping the experience clutter-free and personalized.

**APIs – Integrator Experience**

- **Grant Access to a Reaction Pack:**

  `POST /api/v1/profiles/{profile_uuid}/reaction-packs/`
  Grants access to an exclusive reaction pack for the specified profile.

  ```
  {
      "reaction_pack_id": "6e654321-abcd-4def-9012-9876543210fe",
  }
  ```
- **List All Reaction Packs Owned by Profile**

  Retrieves a paginated list of all reaction packs currently owned by the specified profile.
  `GET /api/v1/profiles/{profile_uuid}/reaction-packs/`
- **Revoke Access to a Reaction Pack**

  Revokes the user's access to a specific reaction pack.<br />`DELETE /api/v1/profiles/{profile_uuid}/reaction-packs/{reaction_pack_id}/`

## Reaction Packs

![](https://files.readme.io/1859c1e-reaction.gif)

A Reaction Pack defines a set of reaction types. Each pack can have many reaction types inside of it, and each type has an ID, name, and image asset. Once a pack is created it can be associated with spaces in order to make its reaction types available inside those spaces.

An application can have multiple reaction packs, and each space can use a some or all of those packs. Mapping packs to content through spaces allows reactions to be curated and dynamic per space, like having limited themed reactions during holidays and big events, or team-specific reactions during sports matches.

#### List Reaction Packs

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

#### Get Reaction Pack Details

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

## Reaction Spaces

Reaction space is a resource which lets you add or remove reactions for a given target. It maps your content unique identifier i.e target group Id with reaction pack Id and also helps in achieving a complete isolation of user reactions across different content. This also gives you an opportunity to get all user reactions based on target group Id without needing the reference of reaction space Id.

Given a reaction use case for a blog post application, where a user could create a blog post, another users could comment on blog posts as well as react on those comments. For this you can create a corresponding Reaction space for each blog post where the blog post Id would be your target group Id and individual comment Id would be your target Id.

#### Create a Reaction Space

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

#### Update a Reaction Space

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

#### Delete a Reaction Space

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

#### List Reaction Spaces

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

#### Get Reaction Space details by reaction space ID

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

#### Get Reaction Space details by target group ID

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

### Real time Reaction Space events

For real time updates of user reactions, use reaction space events.

#### Add User Reaction event

```javascript
function onAddUserReaction(userReaction){
    console.log(userReaction);
}
LiveLike.addReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.ADD_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onAddUserReaction
)

// To remove a added listener function
LiveLike.removeReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.ADD_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onAddUserReaction // earlier added listener function
)
```
```kotlin
reactionSession.subscribeToUserReactionDelegate(<key>, object : UserReactionDelegate { // the key is used to identify the delegate,needs to be a string
                    override fun onReactionAdded(reaction: UserReaction) {
                        
                    }

                    override fun onReactionRemoved(reaction: UserReaction) {
                       
                    }
                })
```
```swift
func reactionSession(_ reactionSession: ReactionSession, didAddReaction reaction: UserReaction)
```

#### Remove User Reaction event

```javascript
function onRemoveUserReaction(userReaction){
    console.log(userReaction);
}
LiveLike.addReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.REMOVE_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onRemoveUserReaction
)

// To remove a added listener function
LiveLike.removeReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.REMOVE_REACTION,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onRemoveUserReaction // earlier added listener function
)
```
```kotlin
reactionSession.subscribeToUserReactionDelegate(<key>, object : UserReactionDelegate {// the key is used to identify the delegate,needs to be a string
                    override fun onReactionAdded(reaction: UserReaction) {
                        
                    }

                    override fun onReactionRemoved(reaction: UserReaction) {
                       
                    }
                })
```
```swift
func reactionSession(_ reactionSession: ReactionSession, didRemoveReaction reaction: UserReaction)
```

#### Reaction Space Update event

This event is triggered whenever a reaction space is updated with its name or reaction pack ids. You may need to use this event to update your reaction list based on updated reaction pack Ids.

```javascript
function onUpdateReactionSpace(eventDetail){
    console.log(eventDetail);
}
LiveLike.addReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.UPDATE_REACTION_SPACE,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onUpdateReactionSpace
)

// To remove a added listener function
LiveLike.removeReactionSpaceEventListener({
    event: LiveLike.ReactionSpaceEvent.UPDATE_REACTION_SPACE,
    reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7"
},
onUpdateReactionSpace // earlier added listener function
)
```
```kotlin
reactionSession.subscribeToReactionSpaceDelegate(<key>, object: ReactionSpaceDelegate {
		ovveride fun onReactionSpaceUpdated(reactionSpace: ReactionSpace){
    
    }
})
```

<Callout icon="📘" theme="info">
  ### Real Time Events (iOS)

  For iOS SDK, please conform to the respective Delegates
</Callout>

### Real Time User Reaction events

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

## User Reactions

A User Reaction is an individual user reaction from one profile to a target within a space.

#### Create Reaction Session

A **Reaction Session** is the interface to interact with a single reaction space exposed by Android and iOS SDKs

```kotlin
val reactionSession = engagementSDK.createReactionSession(<reaction-space-id>,<target-group-id>,errorDelegate)
```
```swift
reactionSession = self.sdk.reaction.createReactionSession(reactionSpace: reactionSpace)
```

<Callout icon="📘" theme="info">
  ### Reaction Sessions on Android and iOS

  The Reaction Session abstraction is only present on the iOS and Android SDKs. Other SDKs can still use reactions but expose them on other interfaces.
</Callout>

#### Add User Reaction

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

#### List User Reactions by target ID

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

#### Count User Reactions by target IDs

Return counts of user reactions grouped by target ID, broken down by reaction type ID within each target ID. Supply multiple target IDs to perform an optimized batch call.

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

#### Remove User Reaction

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
