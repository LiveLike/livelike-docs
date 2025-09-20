---
title: Reactions
deprecated: false
hidden: false
metadata:
  robots: index
---
\<details> \<summary>Reaction Packs API\</summary>
List Reaction Packs
Retrieve all reaction packs created through the Producer Suite.
LiveLike.getReactionPacks().then((\{results}) => console.log(results))
engagementSDK.reaction().getReactionPacks(LiveLikePagination.FIRST,
&#x20;   object : LiveLikeCallback\<List\<ReactionPack>>() \{
&#x20;       override fun onResponse(result: List\<ReactionPack>?, error: String?) \{
&#x20;           result?.let \{
&#x20;               // Handle success
&#x20;           }
&#x20;           error?.let \{
&#x20;               // Handle failure
&#x20;           }
&#x20;       }
&#x20;   })
sdk.reaction.getReactionPacks(page: .first) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionPacks):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
Get Reaction Pack Details
Retrieve details of a reaction pack by its ID.
LiveLike.getReactionPackDetail(\{
&#x20;   reactionPackId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionPack => console.log(reactionPack))
engagementSDK.reaction()
&#x20;   .getReactionPackDetails(\<reaction-pack-id>, object: LiveLikeCallback\<ReactionPack>() \{
&#x20;       override fun onResponse(result: ReactionPack?, error: String?) \{
&#x20;           result?.let \{
&#x20;               // Handle success
&#x20;           }
&#x20;           error?.let \{
&#x20;               // Handle error
&#x20;           }
&#x20;       }
&#x20;   })
sdk.reaction.getReactionPackInfo(reactionPackID: packID) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionPack):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
\</details> \<details> \<summary>Reaction Spaces API\</summary>
Create a Reaction Space
Create a reaction space by linking reaction pack IDs to a target group (unique identifier for content).
LiveLike.createReactionSpace(\{
&#x20;   targetGroupId: "target-group-1",
&#x20;   reactionPackIds: \["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
engagementSDK.reaction()
&#x20;   .createReactionSpace(\<name>, \<target-group-id>, \<list-of-reaction-pack-ids>, object: LiveLikeCallback\<ReactionSpace>() \{
&#x20;       override fun onResponse(result: ReactionSpace?, error: String?) \{
&#x20;           result?.let \{
&#x20;               // Handle success
&#x20;           }
&#x20;           error?.let \{
&#x20;               // Handle failure
&#x20;           }
&#x20;       }
&#x20;   })
sdk.reaction.createReactionSpace(name: reactionSpaceName, targetGroupID: targetGroupID, reactionPackIDs: \[reactionPackIDs]) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionSpace):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
Update a Reaction Space
Update the name or reaction pack IDs of an existing reaction space.
LiveLike.updateReactionSpace(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionPackIds: \["aa7e03fc-01f0-4a98-a2e0-3fed689632d7", "0fddc166-b8c3-4ce9-990e-848bde12188b"]
}).then(reactionSpace => console.log(reactionSpace))
engagementSDK.reaction().updateReactionSpace(\<reaction-space-id>, \<target-group-id>, \<list-of-reaction-pack-ids>, object: LiveLikeCallback\<ReactionSpace>() \{
&#x20;   override fun onResponse(result: ReactionSpace?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
sdk.reaction.updateReactionSpace(reactionSpaceID: spaceID, reactionPackIDs: \[reactionPackID]) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionPackIDList):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
Delete a Reaction Space
LiveLike.deleteReactionSpace(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
})
engagementSDK.reaction().deleteReactionSpace(\<reaction-space-id>, object: LiveLikeCallback\<Unit>() \{
&#x20;   override fun onResponse(result: Unit?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
sdk.reaction.deleteReactionSpace(reactionSpaceID: spaceID) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let success):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
List Reaction Spaces
Get all reaction spaces in an application.
LiveLike.getReactionSpaces().then((\{results}) => console.log(results))
engagementSDK.reaction().getReactionSpaces(\<reaction-space-id>, \<target-group-id>, LiveLikePagination.FIRST, object: LiveLikeCallback\<List\<ReactionSpace>>() \{
&#x20;   override fun onResponse(result: List\<ReactionSpace>?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
sdk.reaction.getReactionSpaces(reactionSpaceID: spaceID, targetGroupID: nil, page: .first) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionSpaces):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
Get Reaction Space Details (by ID)
LiveLike.getReactionSpaceDetail(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
}).then(reactionSpace => console.log(reactionSpace))
engagementSDK.reaction().getReactionSpaceDetails(\<reaction-space-id>, object: LiveLikeCallback\<ReactionSpace>() \{
&#x20;   override fun onResponse(result: ReactionSpace?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
sdk.reaction.getReactionSpaceInfo(reactionSpaceID: spaceID) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionSpace):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
Get Reaction Space Details (by Target Group ID)
Preferred method to avoid storing reaction space IDs.
LiveLike.getReactionSpaceDetail(\{
&#x20;   targetGroupId: "target-group-1",
}).then(reactionSpace => console.log(reactionSpace))
engagementSDK.reaction().getReactionSpaces(\<reaction-space-id>, \<target-group-id>, LiveLikePagination.FIRST, object: LiveLikeCallback\<List\<ReactionSpace>>() \{
&#x20;   override fun onResponse(result: List\<ReactionSpace>?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
sdk.reaction.getReactionSpaces(reactionSpaceID: nil, targetGroupID: targetGroupID, page: .first) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let reactionSpaces):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
\</details> \<details> \<summary>User Reactions API\</summary>
Create Reaction Session
val reactionSession = engagementSDK.createReactionSession(\<reaction-space-id>, \<target-group-id>, errorDelegate)
reactionSession = self.sdk.reaction.createReactionSession(reactionSpace: reactionSpace)
Add User Reaction
Requires: Reaction Space ID, Reaction ID (from a pack), Target ID (unique identifier of item being reacted on)
LiveLike.addUserReaction(\{
&#x20;   targetId: "target-1",
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(reaction => console.log(reaction))
reactionSession.addUserReaction(\<target-id>, \<reaction-id>, \<custom-data>, object: LiveLikeCallback\<UserReaction>() \{
&#x20;   override fun onResponse(result: UserReaction?, error: String?) \{
&#x20;       // Handle response
&#x20;   }
})
reactionSession.addUserReaction(targetID: targetID, reactionID: reactionID, customData: nil) \{ result in
&#x20;   switch result \{
&#x20;     case .success(let userReaction):
&#x20;       // Success block
&#x20;     case .failure(let error):
&#x20;       // Failure block
&#x20;   }
}
List User Reactions (by Target ID)
LiveLike.getUserReactions(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   targetId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
}).then(paginatedReactions => console.log(paginatedReactions))
List User Reactions (by Reaction Type ID)
LiveLike.getUserReactions(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   reactionId: "2gddc166-b8c3-4ce9-990e-52352fskj29"
}).then(paginatedReactions => console.log(paginatedReactions))
Count User Reactions (by Target IDs)
Get reaction counts for up to 20 target IDs in one request.
LiveLike.getUserReactionsCount(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   targetIds: \["0fddc166-b8c3-4ce9-990e-848bde12188b"],
}).then(reaction => console.log(reaction))
Remove User Reaction
Remove a user reaction using its userReactionId.
LiveLike.removeUserReaction(\{
&#x20;   reactionSpaceId: "aa7e03fc-01f0-4a98-a2e0-3fed689632d7",
&#x20;   userReactionId: "0fddc166-b8c3-4ce9-990e-848bde12188b"
})
\</details>
