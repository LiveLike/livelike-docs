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
## User Profile Badges

A user profile badge is a badge that is linked to a user profile. A user profile can have multiple badges that can be earned or awarded. Once a badge is earned or awarded it stays linked to the user profile regardless of any changes done to the badge.

> 📘 How to setup a badge?
>
> Refer [Utilizing Badge](badges#utilizing-badges) documentation.

## Retrieve badges earned or awarded to a user

All the badges that have been earned or awarded to a user profile can be retrieved using the code samples below

**API Definition:** [getProfileBadges](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileBadges)

```javascript
import { getProfileBadges } from '@livelike/javascript'

getProfileBadges({
  profileId: "xxxxxx"
}).then(paginatedResponse => console.log(paginatedResponse.results))
```

## Retrieving user's progress towards earning a badge

A user's progress towards a badge can be retrieved using the code examples below. Since a single badge could be setup to be earned in different ways, multiple badge progressions are linked to a single Badge.

**API Definition:** [getBadgeProgress](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getBadgeProgress)

```javascript
import { getBadgeProgress } from '@livelike/javascript'

getBadgeProgress({
  profileId: "<profile id>",
  badgeIds: ["xxxx", "xxxx"]
}).then(res => console.log(res))
```

## Retrieving all badges linked to an application

As an integrator you have the ability to retrieve all of the badges linked to an application. The results of this call can be used at a later time to query badge progress by passing badge ID's of interest. 

**API Definition:** [getApplicationBadges](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getApplicationBadges)

```javascript
import { getApplicationBadges } from '@livelike/javascript'

getApplicationBadges()
.then(padinatedResponse => console.log(padinatedResponse.results))
```

## Retrieving all profiles for a given badge

As an integrator you have the ability to retrieve all the profiles who have earned a given badge.

**API Definition:** [getBadgeProfiles](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getBadgeProfiles)

```javascript
import { getBadgeProfiles } from '@livelike/javascript'

getBadgeProfiles({
  badgeId: "<badge Id>"
}).then(res => console.log(res))
```
