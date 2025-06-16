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
[block:api-header]
{
  "title": "Creating a Sponsor"
}
[/block]
1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Sponsors" in the Sidebar
3. Select the "New Sponsor" button on the top right hand side
4. Enter Sponsor Name, pick a logo image to upload and select the brand color
5. Select "Create" to finish
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/51db0db-Screenshot_2022-01-20_at_12.25.28_PM.png",
        "Screenshot 2022-01-20 at 12.25.28 PM.png",
        614,
        1182,
        "#595256"
      ],
      "sizing": "smart",
      "border": false
    }
  ]
}
[/block]
At this point you have a sponsor that is ready to be linked to a program.
[block:api-header]
{
  "title": "Linking Sponsor(s) with a Program"
}
[/block]
1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select "Programs" in the Sidebar
3. Select the program you are working with
4. Press on the vertical triple dots button of a program
5. Select "Edit Program"
6. Scroll to the "Linked Sponsors"
7. Select/Unselect the Sponsor you would like to link (use ctrl select for multiple sponsor selections)
8. Press "Update" to update Sponsor link changes that have been made to the program

Now you have Sponsors that are linked to a program. 
[block:api-header]
{
  "title": "Retrieving Application Sponsor(s) in the SDK"
}
[/block]
Get list of all sponsors created in a given application
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getApplicationSponsors()\n.then((paginatedSponsors) => {\n    console.log(paginatedSponsors);\n})",
      "language": "javascript"
    },
    {
      "code": "sdk.sponsorship.getByApplication(page: .first) { result in\n    switch result {\n        case .success(let sponsors):\n            //Success Block\n        case .failure(let error):\n            //Failure Block\n    }\n}",
      "language": "swift"
    },
    {
      "code": "sdk.sponsor().fetchForApplication(LiveLikePagination.FIRST, object : LiveLikeCallback<List<SponsorModel>>() {\n    override fun onResponse(result: List<SponsorModel>?, error: String?) {\n        \n    }\n})",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving Program Sponsor(s) in the SDK"
}
[/block]
Now that you have linked sponsor(s) to a program, you will now be able to retrieve sponsor information through our SDK interfaces.
[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getProgramSponsors({ programId: \"<program id>\"})\n.then(paginatedSponsors => {\n    console.log(paginatedSponsors);\n})",
      "language": "javascript"
    },
    {
      "code": "class HelloWorld {\n  let sdk: EngagementSDK\n  \n  sdk.sponsorship.getBy(programID: <\"progam id\">) { result in\n     switch result {\n     case let .success(let sponsors):\n     \t//do something with sponsors\n     case let .failure(error):\n     \tprint(error)\n     }\n  }\n}",
      "language": "swift"
    },
    {
      "code": "sdk.sponsor().fetchByProgramId(\n    <program-id>,\n    LiveLikePagination.FIRST,\n    object : LiveLikeCallback<List<SponsorModel>>() {\n        override fun onResponse(result: List<SponsorModel>?, error: String?) {\n            \n        }\n    }\n)",
      "language": "kotlin"
    },
    {
      "code": "final sponsorsList =await sdk.sponsor.fetchByProgramId(<program-id>)",
      "language": "text",
      "name": "Flutter"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving Chatroom Sponsor(s) in the SDK"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "LiveLike.getChatRoomSponsors({ roomId: \"room-id\" })\n.then(paginatedSponsors => {\n    console.log(paginatedSponsors);\n})",
      "language": "javascript"
    },
    {
      "code": "self.sdk.sponsorship.getBy(\n    chatRoomID: chatroom.roomID, \n    page: .first, \n    completion: { result in\n        switch result {\n            case .success(let sponsors):\n                //Success Block\n            case .failure(let error):\n                //Failure Block\n        }\n    }\n)",
      "language": "swift"
    },
    {
      "code": "sdk.sponsor().fetchByChatRoomId(\n    <chat-room-id>,\n    LiveLikePagination.FIRST,\n    object : LiveLikeCallback<List<SponsorModel>>() {\n        override fun onResponse(result: List<SponsorModel>?, error: String?) {\n            \n        }\n\n    })",
      "language": "kotlin"
    }
  ]
}
[/block]