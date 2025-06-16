---
title: User Profile Integration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-blocking-profiles
      title: User Profile Moderation
---
The LiveLike profile system can be used to handle a variety of scenarios, ranging from local anonymous experiences to persistent integration with existing user account systems. You can read more about those use cases in the [profiles product guide](doc:user-profiles).
[block:api-header]
{
  "title": "Initializing the SDK"
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "Creating new profiles again may result in higher than expected MAU([Monthly Active User](https://docs.livelike.com/docs/monthly-active-users-maus)) count which can effect billing.",
  "title": "Warning"
}
[/block]
The LiveLike initializer returns a promise that resolves a profile object. Unless an access token is provided, those calls to init will resolve a new profile each time. This may be appropriate for one-off micro experiences, but usually an integration would persist the profile so that it is re-used the next time the SDK is initialized. Here is an example of how this might be managed in a purely client-side integration:

We also recommend that you initialize the SDK as late as possible in your application - just before the user accesses the EngagementSDK features.
[block:code]
{
  "codes": [
    {
      "code": "import {init} from '@livelike/javascript'\n\nif (alreadySavedAccessToken()) {\n  // Already saved an access token: re-use it!\n  const profile = await LiveLike.init({\n    clientId,\n    accessToken: loadSavedAccessToken()\n  });\n} else {\n  // No saved access token yet, save it for next time\n  const profile = await LiveLike.init({ clientId })\n  saveAccessToken(profile.access_token)\n}",
      "language": "javascript"
    }
  ]
}
[/block]
The `alreadySavedAccessToken`, `loadSavedAccessToken` and `saveAccessToken` functions are just placeholders, you can imagine they might store the access token in local storage to be re-used later. A more complex integration might save and load them from your user account service on the backend, for example.
[block:callout]
{
  "type": "danger",
  "title": "Initialization will create a profile if an access token is not provided",
  "body": "Take note that the `init` method will create a new profile if an `accessToken` option is not provided and already existing profile data is not available in localStorage. This can result in duplicate profiles being created if not managed carefully."
}
[/block]

[block:api-header]
{
  "title": "Reusing an Existing Profile"
}
[/block]
If you already have an access token for a LiveLike profile, you can pass it into the init function as `accessToken`. This will load the user profile associated with that access token. This is common when LiveLike access tokens are being stored your own user account records in your backend.
[block:code]
{
  "codes": [
    {
      "code": "import { init } from '@livelike/javascript'\n\nconst existingProfile = await init({\n  accessToken,\n  clientId\n})",
      "language": "javascript"
    }
  ]
}
[/block]