---
title: Getting Started
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
      slug: react-native-core-concepts
      title: Core Concepts
---
> 🚧 Prerequisite
>
> Before getting started with our React Native SDK, we assume you have already setup React Native environment, if not refer official [React Native getting started](https://reactnative.dev/docs/environment-setup) docs.

## React Native SDK

React native SDK has rich set of customisable Stock UI for you to quickly get started.\
It has following peer dependencies:

* @livelike/javascript - This is our Javascript SDK that react native SDK internally uses to connect to our engagement services
* react
* react-native  

> 📘 Supported platform dependencies
>
> react: `^18.1.0`\
> react-native: `^0.70.5`

## Installing React Native SDK

```text npm
npm install -S @livelike/javascript @livelike/react-native
```
```text yarn
yarn add @livelike/javascript @livelike/react-native
```

> 🚧 Peer dependencies conflict
>
> If your application is using react-native v0.70.5+, and you are using npm v7+, during the sdk installation you may encounter NPM throwing an error regarding the conflict of react-native versions.\
> To solve this conflict and install the SDK, use:\
> `npm install -S @livelike/javascript @livelike/react-native --legacy-peer-deps`

> 🚧 GIFs are not supported by default on Android
>
> You will need to add **com.facebook.fresco:animated-gif:2.+** as an additional dependency to **android/app/build.gradle**\
> [Read more...](https://reactnative.dev/docs/0.62/image#gif-and-webp-support-on-android)

> 👍 React native app setup
>
> We support both expo and react native cli app setup

## Initialise React Native SDK

To get started with react native SDK and to use any of the SDK functionality, you need to initialise the SDK with `clientId`.\
You can either use `useInit` hook or [`init` API](javascript-getting-started)  from javascript SDK.

> 📘 Make sure you have a valid Client ID
>
> You'll need a Client ID for this step, which you learn how to do in [Retrieving Important Keys](doc:retrieving-important-keys).

### Using `useInit` hook:

```typescript
import { useInit, LLChat } from '@livelike/react-native';
import { ActivityIndicator } from "react-native";

const myClientId = 'your-app-client-id';

export function MyComponent(){
 const { profile } = useInit({ clientId: myClientId });
 
  if(!profile){
    // return loading UI
    return <ActivityIndicator/>
  }
  // return any React naitve SDK UI component 
  return <LLChat roomId="<your-chat-room-id>"/>
}
```

### Using `init` API:

```typescript
import { init } from '@livelike/javascript';
import { ActivityIndicator } from "react-native";

const myClientId = 'your-app-client-id';

export function MyComponent(){
 const [profile, setProfile ] = useState(null);
 useEffect(() => {
   init({ clientId: myClientId })
   .then(userProfile => {
     setProfile(userProfile);
   })
 }, [])

 if(!profile){
    // return loading UI
    return <ActivityIndicator/>
  }
  // return any React native SDK UI component 
  return <LLChat roomId="<your-chat-room-id>"/>
}
```

### We highly recommend referring [Core Concepts](react-native-core-concepts) section before going through our components and hooks documentation.
