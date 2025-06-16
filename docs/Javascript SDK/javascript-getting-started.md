---
title: Getting started
excerpt: How to get started with the Javascript SDK
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
      slug: javascript-user-profile
      title: User Profile
    - type: basic
      slug: javascript-chat
      title: Chat
    - type: basic
      slug: javascript-reactions
      title: Reactions
---
LiveLike Javascript SDK is an isomorphic package that could be used in any JS runtime environment allowing integrators to enhance user experiences with chat and other features to increase user engagement. JS runtime could be:
1. Web Browser (you could also use `@livelike/engagementsdk` instead)
2. Node.js (server side JS runtime technology)
3. Electron.js (client side technology to develop Desktop Application)
4. React Native (client side technology to develop native IOS and Android Mobile Application)
[block:api-header]
{
  "title": "Installing"
}
[/block]
The Javascript SDK can be installed with npm or Yarn. For more details see the NPM package. 
[block:code]
{
  "codes": [
    {
      "code": "npm i @livelike/javascript",
      "language": "shell",
      "name": "npm"
    },
    {
      "code": "yarn add @livelike/javascript",
      "language": "shell",
      "name": "yarn"
    }
  ]
}
[/block]
Initialize the SDK with the LiveLike.init function. A Client ID is required to be passed as the clientId property of the function's object argument.
[block:callout]
{
  "type": "info",
  "title": "Make sure you have a valid Client ID",
  "body": "You'll need a Client ID for this step, which you learn how to do in [Retrieving Important Keys](doc:retrieving-important-keys)."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import { init } from \"@livelike/javascript\";\n\nimport { clientId } from './your-config'\n \ninit({ clientId }).then(profile => {\n  // This will generate a new profile\n  console.log(\"LiveLike is connected!\")\n});",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Init Argument Details"
}
[/block]
#### `clientId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String (**Required**)",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `accessToken`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `logger`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "boolean",
    "0-1": "false"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `nickName`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "If not provided, nickname will be randomly generated for the new profiles"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `storageStrategy`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[IStorageStrategy]()",
    "0-1": "localStorage"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `publishKey`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `endpoint`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "https://cf-blast.livelikecdn.com/api/v1/"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `analyticsProvider`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[IAnalyticsProvider]()",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "API reference",
  "body": "Browse our [API reference](javascript-api-reference) in case you need to understand API params return data types, API usages, object properties, etc."
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "User Profile Integration",
  "body": "The init function will create a new LiveLike profile and access token by default, and **each profile created counts toward a monthly active user count**. You should re-use the access tokens when you can to treat returning visitors as the same user. To better integrate this into your own product and more accurately reflect your MAUs, check out the [User Profile Integration](doc:web-user-profile-integration) section."
}
[/block]