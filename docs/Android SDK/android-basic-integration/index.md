---
title: Getting Started
excerpt: Get a basic integration up and running with the Android SDK
deprecated: false
hidden: false
metadata:
  title: Basic Integration | Android SDK | Getting Started | LiveLike
  description: >-
    This is a developer's guide for setting up Android SDK configuration for
    native Android apps. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: link
      title: Spoiler Prevention
      url: https://docs.livelike.com/docs/android-spoiler-free
    - type: link
      title: Chat
      url: https://docs.livelike.com/docs/chat-2
    - type: link
      title: Widget Configuration
      url: https://docs.livelike.com/docs/android-widget-config
    - type: link
      title: Analytics
      url: https://docs.livelike.com/docs/android-analytics
    - type: link
      title: Widget Timeline
      url: https://docs.livelike.com/docs/widget-timeline
---
This is a developers' guide for setting up Android Engagement SDK  configuration for native Android apps. We will take you through the basic technical steps for configuration and show you how to send your first widgets and chat messages. We will also provide detailed samples and instructions for complete LiveLike integration.

## Prerequisites

* An admin login and registered application on the [Producer Suite](https://cf-blast.livelikecdn.com/)
* Client ID - Used to initialize the SDK. To get your ClientID, register your application in the [Producer Suite](https://cf-blast.livelikecdn.com/)
* Minimum OS: Android 5.0
* Minimum Android SDK: Lollipop SDK 21

> 🚧 Android X Upgrade
>
> The Android Engagement SDK has been migrated to Android X from 2.15 onwards
>
> If you have any issues with the integration please reach out.

## Installation

<Callout icon="👍" theme="okay">
  Current Version is 3.0.5
</Callout>

**Step 1**\
Add the JitPack repository to your build file

```text Gradle
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

```text Gradle
implementation 'com.livelike.android-engagement-sdk:engagementsdk:<<android-current-version>>'
```
```text Maven
<dependency>
  <groupId>com.livelike.android-engagement-sdk</groupId>
  <artifactId>engagementsdk</artifactId>
  <version> <<android-current-version>> </version>
</dependency>
```
```text sbt
libraryDependencies += "com.livelike.android-engagement-sdk" % "engagementsdk" % "<<android-current-version>>"
```
```text leiningen
:dependencies [[com.livelike.android-engagement-sdk/engagementsdk " <<android-current-version>> "]]
```

> 📘 Artifact name
>
> There has been some change in artifact name since version 2.17, Please make sure while upgrading the version, it matches exactly what mentioned above

## Initialization

For this step, you will need your Client ID to initialize the Android Engagement SDK. See here to [retrieve your Client ID](doc:retrieving-important-keys).

**Note**: The LiveLike SDK generates a User <Glossary> Access Token</Glossary> whenever initialized. You can either choose to store it locally or persist it within your internal user database (although we have already managed it internally in the SDK). The access Token is stored locally which can be updated if the user uninstalls the application or clears data from application settings. This may result in higher MAUs(\[Monthly Active Users], so it is highly recommended to pass the accessToken delegate as a param on SDK init and store the accessToken for persistent users count.\
See [Profiles](doc:user-profiles) for more info.
We also recommend that you initialize the SDK as late as possible in your application - just before the user accesses the EngagementSDK features.

```kotlin
val engagementSDK = EngagementSDK(
            LIVELIKE_CLIENT_ID,
            applicationContext,
            object : ErrorDelegate() {
                override fun onError(error: String) {
                   
                }
            }, accessTokenDelegate = object : AccessTokenDelegate {
                override fun getAccessToken(): String? {
                    return getSharedPreferences(PREFERENCES_APP_ID, Context.MODE_PRIVATE).getString(
                        PREF_USER_ACCESS_TOKEN,
                        null
                    ).apply {
                        
                    }
                }

                override fun storeAccessToken(accessToken: String?) {
                    getSharedPreferences(PREFERENCES_APP_ID, Context.MODE_PRIVATE).edit().putString(
                        PREF_USER_ACCESS_TOKEN, accessToken
                    ).apply()
                }
            })
```
```java
EngagementSDK engagementSDK = new EngagementSDK(
                LIVELIKE_CLIENT_ID,
                applicationContext, null, null,
                new AccessTokenDelegate() {
                    @Nullable
                    @Override
                    public String getAccessToken() {
                        return token;
                    }

                    @Override
                    public void storeAccessToken(@Nullable String accessToken) {
                     // store access token
                    }
                }
        );
```

## Configure Your Layout

Now you have to configure your media page layout and declare containers for the Android Engagement SDK Widget and Chat views to live inside.

<Callout icon="📘" theme="info">
  Even though this guide makes use of both the chat and widget components, if desired it is possible to use only one of the components.
</Callout>

<Callout icon="🚧" theme="warn">
  The width of the Widget view must be at least **292dp** and the width of the Chat view must be at least **292dp**.
</Callout>

Add the following to your layout XML

```xml
<com.livelike.engagementsdk.chat.ChatView
    android:id="@+id/chat_view"
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:minWidth="292dp"
    app:displayUserProfile="true"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintBottom_toBottomOf="parent"/>
            
<com.livelike.engagementsdk.widget.view.WidgetView
    android:id="@+id/widget_view"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:minWidth="292dp"                                               
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"/>
```

Notes:

* The `displayUserProfile` boolean property is used to control the display of the user profile bar above the chat input box.
* Properties of the view can be set via XML or programmatically.

## Start a Content Session

A Content Session represents a user's subscription to a particular program (typically a live, linear TV show, game, or episode). To start a Content Session you will need a **Program ID**. Integrating teams are expected to create programs within the LiveLike system, either through the API or through the Producer Suite. The team should then copy the **Program ID**s into the relevant media metadata in their own systems so that content sessions can be started along with media playback.

**How to retrieve a Program ID:**

<Embed url="https://www.youtube.com/watch?v=eojvteNhogw&feature=youtu.be" href="https://www.youtube.com/watch?v=eojvteNhogw&feature=youtu.be" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FeojvteNhogw%253Ffeature%253Doembed%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DeojvteNhogw%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FeojvteNhogw%252Fhqdefault.jpg%26key%3Df2aa6fc3595946d0afc3d76cbbd25dc3%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

**How to publish a widget:**

<Embed url="https://www.youtube.com/watch?v=W1--cNOHi0g&feature=youtu.be" href="https://www.youtube.com/watch?v=W1--cNOHi0g&feature=youtu.be" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252FW1--cNOHi0g%253Ffeature%253Doembed%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253DW1--cNOHi0g%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252FW1--cNOHi0g%252Fhqdefault.jpg%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

## Starting a Content Session

```kotlin
val contentSession = engagementSDK.createContentSession("<program-id >")
widget_view.setSession(contentSession)
chat_view.setSession(contentSession.chatSession)
```
```java
LiveLikeContentSession session = engagementSDK.createContentSession("<program-id>");
WidgetView widgetView = findViewById(R.id.widgetView);
widgetView.setSession(session);
ChatView chatView = findViewById(R.id.chatView);
chatView.setSession(session);
```

## Handling application going to background

When your application goes to background the Android Engagement SDK is still listening for new widgets to make sure the user doesn't lose any of the action when coming back.

If you want to disable this feature and assure the application remains dormant when backgrounded, you will need to Pause and Resume the Content Session.

```kotlin
// When going to background
contentSession.pause()

// When coming back from background 
contentSession.resume()

// When exiting your activity
contentSession.close()
```
```java
// When going to background
contentSession.pause();

// When coming back from background 
contentSession.resume();

// When exiting your activity
contentSession.close();
```

> 📘 For SDK version 2.63 and above.
>
> The **setWidgetThemeViewAttribute** earlier accessed from Content Session is now moved to Widget View and now can be accessed by **widgetView\.widgetViewThemeAttributes**
>
> The **shouldDisplayedAvatar** earlier accessed from Chat Session is now moved to Chat View and can be accessed by **chatView\.shouldDisplayAvatar = true**
>
> The **setProfilePicUrl** earlier accessed from Content Session, can now be accessed from sdk as **sdk.updateChatUserPic(url)**