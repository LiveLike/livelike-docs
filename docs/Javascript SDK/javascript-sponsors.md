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
Manage sponsorships based on your business requirement using sponsor resource.\
A sponsor is an object that is created on the Application level in the [Producer Site](https://cf-blast.livelikecdn.com/producer). Sponsor maintains a many to many relationship with Programs and Chatrooms which can be managed in the Sponsors section of your application in the [Producer Site](https://cf-blast.livelikecdn.com/producer)

> 📘 How to setup a sponsor?
>
> Refer [Creating a sponsor](sponsorship#creating-a-sponsor) documentation. Based on your requirement, you can either link a sponsor to program, chatroom or widgets from our producer suite.

## Retrieving Application Sponsor(s)

Get list of all sponsors created in a given application

**API Definition:** [getApplicationSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getApplicationSponsors)

```javascript
import { getApplicationSponsors } from "@livelike/javascript"

getApplicationSponsors()
.then((paginatedSponsors) => {
    console.log(paginatedSponsors.results);
})
```

## Retrieving Program Sponsor(s)

Now that you have linked sponsor(s) to a program, you will now be able to retrieve sponsor information through our SDK interfaces.

**API Definition:** [getProgramSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProgramSponsors)

```javascript
import { getProgramSponsors } from "@livelike/javascript"

getProgramSponsors({
  programId: "<program id>"
}).then(paginatedSponsors => console.log(paginatedSponsors.results))
```

## Retrieving Chatroom Sponsor(s)

Retrieve chatroom sponsors

**API Definition:** [getChatRoomSponsors](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getChatRoomSponsors)

```javascript
import { getChatRoomSponsors } from "@livelike/javascript"

getChatRoomSponsors({
  roomId: "room-id"
}).then(paginatedSponsors => console.log(paginatedSponsors.results))
```

## Retrieving Widget Sponsor(s)

Widgets sponsors list is part of widget payload that could be retrieved using [getWidget](javascript-widgets#getwidget) or [getWidgets](javascript-widgets#getwidgets) API.

Refer `sponsors` property in [IWidgetPayload](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IWidgetPayload)
