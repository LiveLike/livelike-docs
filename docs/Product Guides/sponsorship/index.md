---
title: Sponsorship
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Sponsorship | LiveLike Developer Hub | Engagement SDK
  description: >-
    A sponsor is an object that is created on the Application level in the
    Producer Suite. Learn more about creating a sponsor, linking sponsors with a
    program, and more.
  robots: index
next:
  description: ''
---
A sponsor is an object that is created on the Application level in the [Producer Site](https://cf-blast.livelikecdn.com/producer). Sponsor maintains a many to many relationship with Programs and Chatrooms which can be managed in the Sponsors section of your application in the [Producer Site](https://cf-blast.livelikecdn.com/producer)

## Creating a Sponsor

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Sponsors" in the Sidebar
3. Select the "New Sponsor" button on the top right hand side
4. Enter Sponsor Name, pick a logo image to upload and select the brand color
5. Select "Create" to finish

<Image width="smart" src="https://files.readme.io/51db0db-Screenshot_2022-01-20_at_12.25.28_PM.png" />

At this point you have a sponsor that is ready to be linked to a program.

## Linking Sponsor(s) with a Program

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Programs" in the Sidebar
3. Select the program you are working with
4. Press on the vertical triple dots button of a program
5. Select "Edit Program"
6. Scroll to the "Linked Sponsors"
7. Select/Unselect the Sponsor you would like to link (use ctrl select for multiple sponsor selections)
8. Press "Update" to update Sponsor link changes that have been made to the program

Now you have Sponsors that are linked to a program. 

## Retrieving Application Sponsor(s) in the SDK

Get list of all sponsors created in a given application

```javascript
LiveLike.getApplicationSponsors()
.then((paginatedSponsors) => {
    console.log(paginatedSponsors);
})
```
```swift
sdk.sponsorship.getByApplication(page: .first) { result in
    switch result {
        case .success(let sponsors):
            //Success Block
        case .failure(let error):
            //Failure Block
    }
}
```
```kotlin
sdk.sponsor().fetchForApplication(LiveLikePagination.FIRST, object : LiveLikeCallback<List<SponsorModel>>() {
    override fun onResponse(result: List<SponsorModel>?, error: String?) {
        
    }
})
```

## Retrieving Program Sponsor(s) in the SDK

Now that you have linked sponsor(s) to a program, you will now be able to retrieve sponsor information through our SDK interfaces.

```javascript
LiveLike.getProgramSponsors({ programId: "<program id>"})
.then(paginatedSponsors => {
    console.log(paginatedSponsors);
})
```
```swift
class HelloWorld {
  let sdk: EngagementSDK
  
  sdk.sponsorship.getBy(programID: <"progam id">) { result in
     switch result {
     case let .success(let sponsors):
     	//do something with sponsors
     case let .failure(error):
     	print(error)
     }
  }
}
```
```kotlin
sdk.sponsor().fetchByProgramId(
    <program-id>,
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<SponsorModel>>() {
        override fun onResponse(result: List<SponsorModel>?, error: String?) {
            
        }
    }
)
```
```text Flutter
final sponsorsList =await sdk.sponsor.fetchByProgramId(<program-id>)
```

## Retrieving Chatroom Sponsor(s) in the SDK

```javascript
LiveLike.getChatRoomSponsors({ roomId: "room-id" })
.then(paginatedSponsors => {
    console.log(paginatedSponsors);
})
```
```swift
self.sdk.sponsorship.getBy(
    chatRoomID: chatroom.roomID, 
    page: .first, 
    completion: { result in
        switch result {
            case .success(let sponsors):
                //Success Block
            case .failure(let error):
                //Failure Block
        }
    }
)
```
```kotlin
sdk.sponsor().fetchByChatRoomId(
    <chat-room-id>,
    LiveLikePagination.FIRST,
    object : LiveLikeCallback<List<SponsorModel>>() {
        override fun onResponse(result: List<SponsorModel>?, error: String?) {
            
        }

    })
```
