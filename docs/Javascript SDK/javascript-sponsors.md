---
title: Sponsors
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Manage sponsorships based on your business requirement using sponsor resource.
A sponsor is an object that is created on the Application level in the [Producer Site](https://cf-blast.livelikecdn.com/producer). Sponsor maintains a many to many relationship with Programs and Chatrooms which can be managed in the Sponsors section of your application in the [Producer Site](https://cf-blast.livelikecdn.com/producer)
[block:callout]
{
  "type": "info",
  "title": "How to setup a sponsor?",
  "body": "Refer [Creating a sponsor](sponsorship#creating-a-sponsor) documentation. Based on your requirement, you can either link a sponsor to program, chatroom or widgets from our producer suite."
}
[/block]

[block:api-header]
{
  "title": "Retrieving Application Sponsor(s)"
}
[/block]
Get list of all sponsors created in a given application

**API Definition:** [getApplicationSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getApplicationSponsors)
[block:code]
{
  "codes": [
    {
      "code": "import { getApplicationSponsors } from \"@livelike/javascript\"\n\ngetApplicationSponsors()\n.then((paginatedSponsors) => {\n    console.log(paginatedSponsors.results);\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving Program Sponsor(s)"
}
[/block]
Now that you have linked sponsor(s) to a program, you will now be able to retrieve sponsor information through our SDK interfaces.

**API Definition:** [getProgramSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProgramSponsors)
[block:code]
{
  "codes": [
    {
      "code": "import { getProgramSponsors } from \"@livelike/javascript\"\n\ngetProgramSponsors({\n  programId: \"<program id>\"\n}).then(paginatedSponsors => console.log(paginatedSponsors.results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving Chatroom Sponsor(s)"
}
[/block]
Retrieve chatroom sponsors

**API Definition:** [getChatRoomSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getChatRoomSponsors)
[block:code]
{
  "codes": [
    {
      "code": "import { getChatRoomSponsors } from \"@livelike/javascript\"\n\ngetChatRoomSponsors({\n  roomId: \"room-id\"\n}).then(paginatedSponsors => console.log(paginatedSponsors.results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving Widget Sponsor(s)"
}
[/block]
Widgets sponsors list is part of widget payload that could be retrieved using [getWidget](javascript-widgets#getwidget) or [getWidgets](javascript-widgets#getwidgets) API.

Refer `sponsors` property in [IWidgetPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetPayload)