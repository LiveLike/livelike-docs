---
title: Getting started with LiveLikeKotlin
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
This is a developers' guide for setting up LiveLike Kotlin SDK configuration for Kotlin projects. We will walk you through the installation and initialization steps. Kotlin projects could be:
1. Kotlin Server Projects
2. Fire OS / Fire TV
[block:api-header]
{
  "title": "Installation"
}
[/block]

[block:callout]
{
  "type": "success",
  "body": "Current Version is <<android-current-version>>"
}
[/block]
**Step 1**
Add the JitPack repository to your build file
[block:code]
{
  "codes": [
    {
      "code": "allprojects {\n    repositories {\n        ...\n        maven { url 'https://jitpack.io' }\n    }\n}",
      "language": "text",
      "name": "gradle"
    },
    {
      "code": "<repositories>\n  <repository>\n    <id>jitpack.io</id>\n      <url>https://jitpack.io</url>\n  </repository>\n</repositories>",
      "language": "xml",
      "name": "Maven"
    },
    {
      "code": "resolvers += \"jitpack\" at \"https://jitpack.io\"",
      "language": "text",
      "name": "sbt"
    },
    {
      "code": ":repositories [[\"jitpack\" { :url \"https://jitpack.io\" }]]",
      "language": "text",
      "name": "leiningen"
    }
  ]
}
[/block]
**Step 2**
Add the dependency
[block:code]
{
  "codes": [
    {
      "code": "implementation 'com.livelike.android-engagement-sdk:livelike-kotlin:2.64.3'",
      "language": "text",
      "name": "gradle"
    },
    {
      "code": "<dependency>\n  <groupId>com.livelike.android-engagement-sdk</groupId>\n  <artifactId>livelike-kotlin</artifactId>\n  <version> <<android-current-version>> </version>\n</dependency>",
      "language": "xml",
      "name": "Maven"
    },
    {
      "code": "libraryDependencies += \"com.livelike.android-engagement-sdk\" % \"livelike-kotlin\" % \"<<android-current-version>>\"\t",
      "language": "text",
      "name": "sbt"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Initialization"
}
[/block]
For this step, you will need your Client ID to initialize the Kotlin SDK. See here to [retrieve your Client ID](doc:retrieving-important-keys). 

The LiveLikeKotlin object is the access point for all features. You will need:
* A Client ID
* An Access Token

**Access Token**

The LiveLike SDK creates a new LiveLike profile and generates a User <<glossary: Access Token>> whenever initialized and **each profile created counts toward a monthly active user count**. You should re-use the access tokens when you can to treat returning visitors as the same user. It is highly recommended to pass the accessToken delegate as a param on SDK init and store the accessToken for persistent users count.
[block:code]
{
  "codes": [
    {
      "code": "class Initialization {\nvar sdk = LiveLikeKotlin(\n        clientId = \"8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS\",\n        accessTokenDelegate = object:AccessTokenDelegate{\n            override fun getAccessToken(): String? {\n                  return \"access-token\"\n            }\n\n            override fun storeAccessToken(accessToken: String?) {\n\n            }\n\n        },\n        mainDispatcher = Dispatchers.Default\n        }",
      "language": "kotlin"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Start a Content Session"
}
[/block]
A Content Session represents a user's subscription to a particular program (typically a live, linear TV show, game, or episode). To start a Content Session you will need a **Program ID**. Integrating teams are expected to create programs within the LiveLike system, either through the API or through the Producer Suite. The team should then copy the **Program ID**s into the relevant media metadata in their own systems so that content sessions can be started along with media playback.
[block:code]
{
  "codes": [
    {
      "code": "val contentSession = sdk.createContentSession(\n        programId = \"09d93835-ee52-4757-976c-ea09d6a5798c\",\n        timecodeGetter = object:LiveLikeKotlin.TimecodeGetterCore{\n            override fun getTimecode(): EpochTime {\n                return EpochTime(0)\n            }\n\n        },\n        mainDispatcher = Dispatchers.Default, // if you are not using coroutinesDispatchers.Main, you don't have to provide uiDispatchers & chatUiDispatchers\n        chatMainDispatcher = Dispatchers.Default\n    )\n    ",
      "language": "kotlin"
    }
  ]
}
[/block]
*Note* EochTime enables you to publish spoiler-free content with the SDK. To enable sync, you will need to provide a value (EpochTime) that represents the date/time of your media player's current playback position.

To enable sync, include EpochTime, which returns the current live timecode.