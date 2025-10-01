---
title: Getting Started
excerpt: How to get started with the Web SDK
deprecated: false
hidden: false
metadata:
  title: Getting Started | Web SDK | LiveLike Developer Hub
  description: >-
    The LiveLike SDK allows integrators to enhance their web video experiences
    with chat, interactive widgets, and other features.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: retrieving-important-keys
      title: Retrieving Important Keys
    - type: basic
      slug: web-widgets
      title: Widgets
    - type: basic
      slug: web-chat
      title: Chat
    - type: link
      title: User Profile Integration
      url: https://docs.livelike.com/docs/web-user-profile-integration
---
The LiveLike Engagement SDK allows integrators to enhance their web video experiences with chat, interactive widgets, and other features to increase user engagement.

## Installing

The Engagment SDK can be installed with npm or Yarn. For more details see the [NPM package](https://www.npmjs.com/package/@livelike/engagementsdk).

```shell npm
npm i @livelike/engagementsdk
```

Initialize the SDK with the `LiveLike.init` function. A <Glossary>Client ID</Glossary> is required to be passed as the `clientId` property of the function's object argument.

> 👍 Make sure you have a valid Client ID
>
> You'll need a Client ID for this step, which you learn how to do in [Retrieving Important Keys](doc:retrieving-important-keys).

```javascript
import LiveLike from "@livelike/engagementsdk";

import { clientId } from './your-config'
 
LiveLike.init({ clientId }).then(profile => {
  // This will generate a new profile
  console.log("LiveLike is connected!")
});
```

> 🚧 User Profile Integration
>
> The init function will create a new LiveLike profile and access token by default, and **each profile created counts toward a monthly active user count**. You should re-use the access tokens when you can to treat returning visitors as the same user. To better integrate this into your own product and more accurately reflect your MAUs, check out the [User Profile Integration](doc:web-user-profile-integration) section.
