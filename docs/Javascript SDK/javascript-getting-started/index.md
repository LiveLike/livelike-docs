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

## Installing

The Javascript SDK can be installed with npm or Yarn. For more details see the NPM package. 

```shell npm
npm i @livelike/javascript
```
```shell yarn
yarn add @livelike/javascript
```

Initialize the SDK with the LiveLike.init function. A Client ID is required to be passed as the clientId property of the function's object argument.

> 📘 Make sure you have a valid Client ID
>
> You'll need a Client ID for this step, which you learn how to do in [Retrieving Important Keys](doc:retrieving-important-keys).

```javascript JavaScript
import { init } from "@livelike/javascript";

import { clientId } from './your-config'
 
init({ clientId }).then(profile => {
  // This will generate a new profile
  console.log("LiveLike is connected!")
});
```

## Init Argument Details

#### `clientId`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String (**Required**)
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

#### `accessToken`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

#### `logger`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        boolean
      </td>

      <td>
        false
      </td>
    </tr>
  </tbody>
</Table>

#### `nickName`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String
      </td>

      <td>
        If not provided, nickname will be randomly generated for the new profiles
      </td>
    </tr>
  </tbody>
</Table>

#### `storageStrategy`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [IStorageStrategy]()
      </td>

      <td>
        localStorage
      </td>
    </tr>
  </tbody>
</Table>

#### `publishKey`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

#### `endpoint`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        String
      </td>

      <td>
        [https://cf-blast.livelikecdn.com/api/v1/](https://cf-blast.livelikecdn.com/api/v1/)
      </td>
    </tr>
  </tbody>
</Table>

#### `analyticsProvider`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        [IAnalyticsProvider]()
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

> 📘 API reference
>
> Browse our [API reference](javascript-api-reference) in case you need to understand API params return data types, API usages, object properties, etc.

> 🚧 User Profile Integration
>
> The init function will create a new LiveLike profile and access token by default, and **each profile created counts toward a monthly active user count**. You should re-use the access tokens when you can to treat returning visitors as the same user. To better integrate this into your own product and more accurately reflect your MAUs, check out the [User Profile Integration](doc:web-user-profile-integration) section.
