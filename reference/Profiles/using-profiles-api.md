---
title: Using Profiles
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
A profile collects all the widgets interactions and chat memberships of a single user. A profile has a unique identifier `id`, a non-unique display name `nickname`, and an API credential called an `access_token`. When acting as a specific profile, the access token must be included in the request.
[block:callout]
{
  "type": "info",
  "title": "The profile works with your existing user data",
  "body": "A profile does not have to be treated as the canonical user record for your app. Profiles have been designed to be used like enhancements or extensions of your existing user records. When a profile is created, its ID and access token should be stored with your existing user data."
}
[/block]