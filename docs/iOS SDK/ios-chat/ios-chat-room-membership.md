---
title: Chat Room Membership (iOS)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Chat Room Membership | iOS SDK | LiveLike Developer Hub
  description: >-
    Chat Room Membership is a simple concept of a relationship between a user
    and a chat room. Learn more about iOS Chat Room Membership.
  robots: index
next:
  description: ''
---
Chat Room Membership is a simple concept of a relationship between a user and a chat room. With the functions mentioned below you will have the ability to build out a fully fleshed out chat experience. You will be able to create, delete chat room memberships, in addition you be able to retrieve all rooms a user is a member of and get all memberships in a room. 

A sample implementation of the Chat Room Membership experience can be found in our [Sample App](https://github.com/LiveLike/engagement-sample-app) under the **Create / Join Chat Room** option.

## Create Chat Room Membership

In order for a user to become a member of a chat room, a membership between the two needs to be created. This can be achieved by calling the `createUserChatRoomMembership(roomID: String, completion: @escaping (Result<ChatRoomMember, Error>) -> Void)` function.  When successful, a membership between the room referenced by the `roomID` parameter and the user referenced by the already established `AccessToken` is created.

```swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.createUserChatRoomMembership(roomID: "<room id>") { [weak self] result in
        guard let self = self else { return }
        switch result {
        case .success:
            print("Successfuly created a membership")
        case let .failure(error):
            print("Error \(error.localizedDescription)")
        }
     }
   }
}
```

## Delete Chat Room Membership

The deletion of a chat room membership signifies the end of the user's relationship with a chat room. This can be achieved by calling `deleteUserChatRoomMembership(roomID: String, completion: @escaping (Result<Bool, Error>) -> Void)` function. 

```swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.deleteUserChatRoomMembership(roomID: "<room id>") { [weak self] result in
        guard let self = self else { return }
        switch result {
        case .success:
            print("Successfuly deleted a membership")
        case let .failure(error):
            print("Error \(error.localizedDescription)")
        }
    }
   }
}
```

## Get User's Chat Room Memberships

In order to retrieve all the chat rooms a user is currently a member of, use `getUserChatRoomMemberships(page: ChatRoomMembershipPagination, completion: @escaping (Result<[ChatRoomInfo], Error>) -> Void)` function. As a result you will get an array of `ChatRoomInfo` objects. This functionality is especially useful when building out a chat room picker. 

> 📘 Pagination
> 
> The `getUserChatRoomMemberships` accepts a `ChatRoomMembershipPagination` parameter. Use this parameter to request the **first**, **next** or **previous** page of results.

```swift
class SomeClass {
    let sdk: EngagementSDK
  
    func someMethod(){
        sdk.getChatRoomMemberships(
            options: GetChatRoomMembershipsRequestOptions(
                roomID: "<chat-room-id>",
                profileIDs: ["<profile_id>"]
            ),
            page: .first
        ) { result in
            switch result {
            case let .success(chatRoomMembers):
                print("User is a Member of # Rooms \(chatRoomMembers.count)") 
            case let .failure(error):
                print("Error: \(error.localizedDescription)")
        }
    }
}
```

## Retrieve Memberships for a Chat Room

In order to retrieve all chat room memberships for a specific chat room, use the `getChatRoomMemberships(options: GetChatRoomMembershipsRequestOptions, page: ChatRoomMembershipPagination, completion: @escaping (Result<[ChatRoomMember], Error>) -> Void)` function. As a result you will get an array of `ChatRoomMember` objects. `GetChatRoomMembershipsRequestOptions` enables filtering by chat room id and profile id(s).

> 📘 Pagination
> 
> The `getChatRoomMemberships` accepts a `ChatRoomMembershipPagination` parameter. Use this parameter to request the **first**, **next** or **previous** page of results.

```swift
class SomeClass {
    let sdk: EngagementSDK
  
    func someMethod(){
        sdk.getChatRoomMemberships(
            options: GetChatRoomMembershipsRequestOptions(
              	roomID: "<chat-room-id>"
                profileIDs: ["<profile-id>"]            
            ),
            page: .first
        ) { result in
            switch result {
            case let .success(chatRoomMembers):
                print("Members in Chat Room \(chatRoomMembers.count)")
            case let .failure(error):
                print("Error: \(error.localizedDescription)")
            }
        }
    }
}
```