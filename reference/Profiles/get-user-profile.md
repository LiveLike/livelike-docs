---
title: Get User Profile
excerpt: ''
api:
  file: profiles.json
  operationId: get-user-profile
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This endpoint will respond with the details of a given profile.

> 🚧 Use the Earned Badges API to list someone's badges
>
> Use the [List Earned Badges](ref:get-users-badges) API to list the badges belonging to a profile. The `badges_url` field in the profile object will return the same results as the List Earned Badges API. The `badges` object on the profile will always return an empty list.