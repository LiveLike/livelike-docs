---
title: Badges
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Javascript SDK Badges | LiveLike Developer Hub
  description: >-
    This document provides information on user profile badges, including how to
    set up a badge, retrieve badges earned by a user, retrieve a user's progress
    towards earning a badge, retrieve all badges linked to an application, and
    retrieve all profiles for a given badge.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "User Profile Badges"
}
[/block]
A user profile badge is a badge that is linked to a user profile. A user profile can have multiple badges that can be earned or awarded. Once a badge is earned or awarded it stays linked to the user profile regardless of any changes done to the badge.
[block:callout]
{
  "type": "info",
  "title": "How to setup a badge?",
  "body": "Refer [Utilizing Badge](badges#utilizing-badges) documentation."
}
[/block]

[block:api-header]
{
  "title": "Retrieve badges earned or awarded to a user"
}
[/block]
All the badges that have been earned or awarded to a user profile can be retrieved using the code samples below

**API Definition:** [getProfileBadges](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileBadges)
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileBadges } from '@livelike/javascript'\n\ngetProfileBadges({\n  profileId: \"xxxxxx\"\n}).then(paginatedResponse => console.log(paginatedResponse.results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving user's progress towards earning a badge"
}
[/block]
A user's progress towards a badge can be retrieved using the code examples below. Since a single badge could be setup to be earned in different ways, multiple badge progressions are linked to a single Badge.

**API Definition:** [getBadgeProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getBadgeProgress)
[block:code]
{
  "codes": [
    {
      "code": "import { getBadgeProgress } from '@livelike/javascript'\n\ngetBadgeProgress({\n  profileId: \"<profile id>\",\n  badgeIds: [\"xxxx\", \"xxxx\"]\n}).then(res => console.log(res))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving all badges linked to an application"
}
[/block]
As an integrator you have the ability to retrieve all of the badges linked to an application. The results of this call can be used at a later time to query badge progress by passing badge ID's of interest. 

**API Definition:** [getApplicationBadges](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getApplicationBadges)
[block:code]
{
  "codes": [
    {
      "code": "import { getApplicationBadges } from '@livelike/javascript'\n\ngetApplicationBadges()\n.then(padinatedResponse => console.log(padinatedResponse.results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Retrieving all profiles for a given badge"
}
[/block]
As an integrator you have the ability to retrieve all the profiles who have earned a given badge.

**API Definition:** [getBadgeProfiles](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getBadgeProfiles)
[block:code]
{
  "codes": [
    {
      "code": "import { getBadgeProfiles } from '@livelike/javascript'\n\ngetBadgeProfiles({\n  badgeId: \"<badge Id>\"\n}).then(res => console.log(res))",
      "language": "javascript"
    }
  ]
}
[/block]