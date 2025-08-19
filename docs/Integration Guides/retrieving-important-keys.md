---
title: Retrieving Important Keys
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Retrieving Important Keys | LiveLike Developer Hub
  description: >-
    When using the LiveLike SDKs and REST APIs, there are a couple IDs and keys
    that you will need. Learn more about retrieving important keys.
  robots: index
next:
  description: ''
---
When using the LiveLike SDKs and REST APIs, there are a couple IDs and keys that you will need. Here we will show you how to retrieve your Client ID, Program IDs and API Access Token.

## Retrieving Client ID

The Client ID is used by both the SDKs and REST APIs to point them to the appropriate application. To retrieve your client ID:

1. Login to the [Producer Suite](https://cf-blast.livelikecdn.com/)
2. Under your profile picture select 'My Organizations' from the dropdown menu.
3. You will see your Client ID under the app available in the 'Apps' section. *If you don't have any apps, use the plus button in the top-right to create a new one.*

![2880](https://files.readme.io/d03b3ba-Screen_Shot_2020-04-06_at_10.46.47_AM.png "Screen Shot 2020-04-06 at 10.46.47 AM.png")

## Retrieving Client Secret

The application client secret is used to sign client-generated user access tokens.  Access tokens generated and signed with the application secret key can contain a `custom_profile_id` in another system that will map to a user profile in LiveLike's system.  This can be used if the integrator system is not able to store the LiveLike user profile IDs or access tokens.

> ❗️ Do not expose your application's Client Secret
>
> The Client Secret is a secret value known only to LiveLike and your own backend system.  Do not embed it in your client application or expose it anywhere in your API.  Doing so could allow someone to generate access tokens for any user in your system and impersonate that user.

## Retrieving Program ID

To access content for a specific <Glossary>Program</Glossary>, you will need the program ID. You can retrieve the Program ID via our REST API or from the [Producer Suite](https://cf-blast.livelikecdn.com/) using the following steps:

1. Login to the [Producer Suite](https://cf-blast.livelikecdn.com/)
2. Open the Event Management Panel (hamburger menu on the top-left).
3. Click the vertical ellipse for your desired program
4. Select "View Program ID"

![2880](https://files.readme.io/6df8f20-Screen_Shot_2020-04-06_at_10.53.41_AM.png "Screen Shot 2020-04-06 at 10.53.41 AM.png")

## Retrieving API Access Token

You will need an API Access Token to access the LiveLike REST APIs. Unlike the user access tokens mentioned in [Profiles](doc:user-profiles), these access tokens have greater privileges that give you full API . To create & retrieve your access token:

1. Login to the [Producer Suite](https://cf-blast.livelikecdn.com/)
2. Under your profile picture select 'My Organizations' from the dropdown menu
3. Select the desired App from your App list
4. Scroll down to API Access Tokens and click "+" to create a new access token

![1440](https://files.readme.io/1d78c34-Screen_Recording_2020-04-06_at_12.10_PM.gif "Screen Recording 2020-04-06 at 12.10 PM.gif")