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
[block:callout]
{
  "type": "warning",
  "title": "Prerequisite",
  "body": "Before getting started with our React Native SDK, we assume you have already setup React Native environment, if not refer official [React Native getting started](https://reactnative.dev/docs/environment-setup) docs."
}
[/block]

[block:api-header]
{
  "title": "React Native SDK"
}
[/block]
React native SDK has rich set of customisable Stock UI for you to quickly get started.
It has following peer dependencies:
* @livelike/javascript - This is our Javascript SDK that react native SDK internally uses to connect to our engagement services
* react
* react-native  
[block:callout]
{
  "type": "info",
  "title": "Supported platform dependencies",
  "body": "react: `^18.1.0`\nreact-native: `^0.70.5`"
}
[/block]

[block:api-header]
{
  "title": "Installing React Native SDK"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "npm install -S @livelike/javascript @livelike/react-native",
      "language": "text",
      "name": "npm"
    },
    {
      "code": "yarn add @livelike/javascript @livelike/react-native",
      "language": "text",
      "name": "yarn"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Peer dependencies conflict",
  "body": "If your application is using react-native v0.70.5+, and you are using npm v7+, during the sdk installation you may encounter NPM throwing an error regarding the conflict of react-native versions.\nTo solve this conflict and install the SDK, use: \n`npm install -S @livelike/javascript @livelike/react-native --legacy-peer-deps`"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "GIFs are not supported by default on Android",
  "body": "You will need to add **com.facebook.fresco:animated-gif:2.+** as an additional dependency to **android/app/build.gradle**\n[Read more...](https://reactnative.dev/docs/0.62/image#gif-and-webp-support-on-android)"
}
[/block]

[block:callout]
{
  "type": "success",
  "title": "React native app setup",
  "body": "We support both expo and react native cli app setup"
}
[/block]

[block:api-header]
{
  "title": "Initialise React Native SDK"
}
[/block]
To get started with react native SDK and to use any of the SDK functionality, you need to initialise the SDK with `clientId`.
You can either use `useInit` hook or [`init` API](javascript-getting-started)  from javascript SDK.
[block:callout]
{
  "type": "info",
  "body": "You'll need a Client ID for this step, which you learn how to do in [Retrieving Important Keys](doc:retrieving-important-keys).",
  "title": "Make sure you have a valid Client ID"
}
[/block]
### Using `useInit` hook:
[block:code]
{
  "codes": [
    {
      "code": "import { useInit, LLChat } from '@livelike/react-native';\nimport { ActivityIndicator } from \"react-native\";\n\nconst myClientId = 'your-app-client-id';\n\nexport function MyComponent(){\n const { profile } = useInit({ clientId: myClientId });\n \n  if(!profile){\n    // return loading UI\n    return <ActivityIndicator/>\n  }\n  // return any React naitve SDK UI component \n  return <LLChat roomId=\"<your-chat-room-id>\"/>\n}",
      "language": "typescript"
    }
  ]
}
[/block]
### Using `init` API:
[block:code]
{
  "codes": [
    {
      "code": "import { init } from '@livelike/javascript';\nimport { ActivityIndicator } from \"react-native\";\n\nconst myClientId = 'your-app-client-id';\n\nexport function MyComponent(){\n const [profile, setProfile ] = useState(null);\n useEffect(() => {\n   init({ clientId: myClientId })\n   .then(userProfile => {\n     setProfile(userProfile);\n   })\n }, [])\n\n if(!profile){\n    // return loading UI\n    return <ActivityIndicator/>\n  }\n  // return any React native SDK UI component \n  return <LLChat roomId=\"<your-chat-room-id>\"/>\n}",
      "language": "typescript"
    }
  ]
}
[/block]

### We highly recommend referring [Core Concepts](react-native-core-concepts) section before going through our components and hooks documentation.