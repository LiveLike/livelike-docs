---
title: Working with LiveLike web experience
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

A LiveLike web experience is created and hosted by LiveLike. A default URL format is `https://client.livelikeapp.com` This experience is designed to work on desktop, mobile web, and mobile native platforms as a web view. While it can function for anonymous users, the recommended approach is to pass a user's identity.

# LiveLike user profiles

Profiles collect user activity across chat, widgets, and other features under a single identity. Upon creation, each profile receives a unique ID and an Access Token. If not provided, a nickname is automatically assigned.

**Further Reading:**

- [Profiles](doc:user-profiles)
- [Custom Profile IDs](doc:custom-profile-ids)

# Creating LiveLike user profiles for your users

Before creating a LiveLike user profile, it's crucial to identify your user's unique identifier. This identifier will be used during the LiveLike user profile creation process to establish a two-way mapping between your user and their LiveLike user profile.

There are two ways to create LiveLike user profiles for your users: 

1. Using the [Create Profile by Custom ID](https://docs.livelike.com/reference/create-profile-by-custom-id) endpoint to generate a LiveLike user profile. This endpoint returns data including an access token, which can be used to authenticate a user in the web experience later.
2. Generating an Access Token for your users [Client-generated Access Tokens](https://docs.livelike.com/docs/client-generated-access-tokens).

# Passing your user’s identity to the LiveLike web experience

A LiveLike web experience can ingest a user's identity by receiving a LiveLike user profile access token. This token is passed as a URL parameter into the experience like so: `https://client.livelikeapp.com/experience.html?accessToken=LIVELIKE_ACCESS_TOKEN`

Consequently, the web experience will be personalized for the user, allowing them to seamlessly continue their activity.