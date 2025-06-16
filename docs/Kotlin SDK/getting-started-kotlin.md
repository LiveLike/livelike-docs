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

## Installation

> 👍 Current Version is {user["android-current-version"]}

**Step 1**\
Add the JitPack repository to your build file

```text gradle
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}
```
```xml Maven
<repositories>
  <repository>
    <id>jitpack.io</id>
      <url>https://jitpack.io</url>
  </repository>
</repositories>
```
```text sbt
resolvers += "jitpack" at "https://jitpack.io"
```
```text leiningen
:repositories [["jitpack" { :url "https://jitpack.io" }]]
```

**Step 2**\
Add the dependency

```text gradle
implementation 'com.livelike.android-engagement-sdk:livelike-kotlin:2.64.3'
```
```xml Maven
<dependency>
  <groupId>com.livelike.android-engagement-sdk</groupId>
  <artifactId>livelike-kotlin</artifactId>
  <version> <<android-current-version>> </version>
</dependency>
```
```text sbt
libraryDependencies += "com.livelike.android-engagement-sdk" % "livelike-kotlin" % "<<android-current-version>>"
```

## Initialization

For this step, you will need your Client ID to initialize the Kotlin SDK. See here to [retrieve your Client ID](doc:retrieving-important-keys). 

The LiveLikeKotlin object is the access point for all features. You will need:

* A Client ID
* An Access Token

**Access Token**

The LiveLike SDK creates a new LiveLike profile and generates a User <Glossary> Access Token</Glossary> whenever initialized and **each profile created counts toward a monthly active user count**. You should re-use the access tokens when you can to treat returning visitors as the same user. It is highly recommended to pass the accessToken delegate as a param on SDK init and store the accessToken for persistent users count.

```kotlin
class Initialization {
var sdk = LiveLikeKotlin(
        clientId = "8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS",
        accessTokenDelegate = object:AccessTokenDelegate{
            override fun getAccessToken(): String? {
                  return "access-token"
            }

            override fun storeAccessToken(accessToken: String?) {

            }

        },
        mainDispatcher = Dispatchers.Default
        }
```

## Start a Content Session

A Content Session represents a user's subscription to a particular program (typically a live, linear TV show, game, or episode). To start a Content Session you will need a **Program ID**. Integrating teams are expected to create programs within the LiveLike system, either through the API or through the Producer Suite. The team should then copy the **Program ID**s into the relevant media metadata in their own systems so that content sessions can be started along with media playback.

```kotlin
val contentSession = sdk.createContentSession(
        programId = "09d93835-ee52-4757-976c-ea09d6a5798c",
        timecodeGetter = object:LiveLikeKotlin.TimecodeGetterCore{
            override fun getTimecode(): EpochTime {
                return EpochTime(0)
            }

        },
        mainDispatcher = Dispatchers.Default, // if you are not using coroutinesDispatchers.Main, you don't have to provide uiDispatchers & chatUiDispatchers
        chatMainDispatcher = Dispatchers.Default
    )
```

*Note* EochTime enables you to publish spoiler-free content with the SDK. To enable sync, you will need to provide a value (EpochTime) that represents the date/time of your media player's current playback position.

To enable sync, include EpochTime, which returns the current live timecode.
