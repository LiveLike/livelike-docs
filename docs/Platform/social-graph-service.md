---
title: Social Graph
excerpt: >-
  Define relationships between users and use them to personalize their
  experience
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Social Graph is an API-first service that enables products to define and explore the social connections between their users and then use those relationships to personalize features. As a product developer using the Social Graph service, you will be able to:

* Create and query connections between your users
* Define your own relationship types like followers, friends, classmates, or anything else
* Discover and analyze connections in your network of users
* Integrate with your existing features and user data

## Social Graph basics

The Social Graph system can be thought of a graph where the nodes are Profiles and the edges are the relationships between profiles.

* A **Profile Relationship** represents a connection between two profiles. Each relationship consists of a _from profile_, a _to profile_, and a _relationship type_. A profile relationship is essentially a directed edge of the given type from one profile to another. Two profiles can share more than one relationship as long as the type is unique between them.
* A **Relationship Type** represents a kind of possible relationship between profiles. Each type has a unique _key_ that is used when creating relationships between profiles. A common relationship type is "follows" but you can define your own types like "studies with" or "rival of."

## Social Graph client

On iOS and Android SDKs the social graph functionality is exposed on a social graph client instance. On the other SDKs functionality is exposed on the LiveLike SDK instance.

```kotlin
socialGraphClient = (application as LiveLikeApplication).sdk.socialGraphClient()
```
```swift
let sdk: EngagementSDK
sdk.socialGraphClient
```
```javascript
import LiveLike from "@livelike/engagementsdk";
```

## Creating relationship types

All relations between profiles must fall into a predefined relationship type. New relationship types can be created via the [Create a Relationship Type](ref:create-a-relationship-type-1) endpoint, and existing ones can be queried via the client interface.

```kotlin
socialGraphClient.getProfileRelationshipTypes(
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<ProfileRelationshipType>>(){
        override fun onResponse(result: List<ProfileRelationshipType>?, error: String?) {
            ...
        }
    }
)
```
```swift
let sdk: EngagementSDK
sdk.socialGraphClient.getProfileRelationshipTypes(
	page: .first,
  options: nil
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let relationshipTypes):
   	// handle success        
   }
}
```
```javascript
LiveLike.getProfileRelationshipTypes().then(({results}) => console.log(results))
```

## Querying relationships

Using the client you can query relationships by any combination of the three parameters `to profile`, `relationship type` and `from profile`

This is an example to find who is following me

```kotlin
socialGraphClient.getProfileRelationships(
    GetProfileRelationshipsRequestParams(
        relationshipTypeKey = "follow",
        toProfileId = "my profile id",
    ),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<ProfileRelationship>>() {
        override fun onResponse(
            result: List<ProfileRelationship>?,
            error: String?
        ) {
            ...
        }
    }
)
```
```swift
let sdk: EngagementSDK
let requestOptions = GetProfileRelationshipsOptions(
  relationshipTypeKey: "follow",
  fromProfileID: nil,
  toProfileID: "my profile ID"
)

sdk.socialGraphClient.getProfileRelationships(
	page: .first,
  options: requestOptions
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let relationshipTypes):
   	// handle success        
   }
}
```
```javascript
LiveLike.getProfileRelationships({
   relationshipTypeKey: "follow",
   toProfileId: "<Profile ID>",
 }).then(({results}) => console.log(results))
```

This example is who am I following

```kotlin
socialGraphClient.getProfileRelationships(
    GetProfileRelationshipsRequestParams(
        fromProfileId = "my profile id",
        relationshipTypeKey = "follow",
    ),
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<ProfileRelationship>>() {
        override fun onResponse(
            result: List<ProfileRelationship>?,
            error: String?
        ) {
            ...
        }
    }
)
```
```swift
let sdk: EngagementSDK
let requestOptions = GetProfileRelationshipsOptions(
  relationshipTypeKey: "follow",
  fromProfileID: "my profile ID",
  toProfileID: nil
)

sdk.socialGraphClient.getProfileRelationships(
	page: .first,
  options: requestOptions
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let relationshipTypes):
   	// handle success        
   }
}
```
```javascript
LiveLike.getProfileRelationships({
   relationshipTypeKey: "follow",
   fromProfileId: "<Profile ID>",
 }).then(({results}) => console.log(results))
```

## Managing relationships

Creating relationships is done one at a time via the client interface

```kotlin
socialGraphClient.createProfileRelationship(
    CreateProfileRelationshipRequestParams(
        fromProfileId = "my profile id",
        relationshipTypeKey = "follow",
        toProfileId = "profile id i'm following",
    ),
    object : LiveLikeCallback<ProfileRelationship> (){
        override fun onResponse(result: ProfileRelationship?, error: String?) {
            ...
        }
    }
)
```
```swift
let sdk: EngagementSDK
let requestOptions = CreateProfileRelationshipOptions(
  fromProfileID: "source profile ID",
  toProfileID: "target profile ID",
  relationshipTypeKey: "follow"
)

sdk.socialGraphClient.createProfileRelationship(
  options: requestOptions
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let relationshipTypes):
   	// handle success        
   }
}
```
```javascript
LiveLike.createProfileRelationship({
   relationshipTypeKey: "follow",
   toProfileId: "<Profile ID>",
   fromProfileId: "<Profile ID>",
 }).then((profileRelationship) => console.log(profileRelationship))
```

> 🚧 Create your relationship types before creating relationships
>
> A relationship type key must exist before it can be used to define relationships between profiles. Use the [Create a Relationship Type](ref:create-a-relationship-type-1) endpoint to create one.

Deleting relationships is similarly achieved via the client interface

```kotlin
socialGraphClient.deleteProfileRelationship(
    DeleteProfileRelationshipsRequestParams( "id of relationship" ),
    object : LiveLikeCallback<LiveLikeEmptyResponse> (){
        override fun onResponse(result: LiveLikeEmptyResponse?, error: String?) {
            ...
        }
    }
)
```
```swift
let sdk: EngagementSDK
let requestOptions = DeleteProfileRelationshipOptions(
  profileRelationshipID: "profile relationship ID to delete"
)

sdk.socialGraphClient.deleteProfileRelationship(
  options: requestOptions
) { result in
   
   switch result {
   case .failure(let error):
   	// handle error             
   case .success(let relationshipTypes):
   	// handle success        
   }
}
```
```javascript
LiveLike.deleteProfileRelationship({ relationshipId: "<Profile Relationship ID>" })
```
