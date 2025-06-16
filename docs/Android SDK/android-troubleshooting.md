---
title: Troubleshooting
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Troubleshooting | Android SDK | LiveLike Developer Hub
  description: >-
    The Android Engagement SDK gives you control over the types of logs that are
    prints. Learn more about Android troubleshooting.
  robots: index
next:
  description: ''
---
## Logging & Debugging

The Engagement SDK gives you control over the types of logs that are printed. This can be helpful to debug unexpected behavior or for reporting a bug to [support@livelike.com](mailto:support@livelike.com). The different logging levels are:

* **Verbose** - Highly detailed level of logging, best used when trying to understand the working of a specific section/feature of the Engagement SDK.
* **Debug** - Information that is diagnostically helpful to integrators and Engagement SDK developers.
* **Info** - Information that is always useful to have, but not vital.
* **Warning** - Information related to events that could potentially cause oddities, but the Engagement SDK will continue working as expected.
* **Error** - An error occurred that is fatal to a specific operation/component, but not the overall Engagement SDK.
* **Severe** - A fatal issue occurred, from which the Engagement SDK cannot recover.
* **None** - No logging enabled.

The default level is **None**.

```kotlin
SDKLogger.minimumLogLevel = LogLevel.Verbose
```
```java
SDKLoggerKt.setMinimumLogLevel(LogLevel.Verbose);
```

You also have the ability to add your own listener for the logs.

```kotlin
registerLogsHandler(object : (String) -> Unit {
  override fun invoke(text: String) {
    // Do something with the log here
  }
})
```
```java
SDKLoggerKt.registerLogsHandler(new Function1<String, Unit>() {
            @Override
            public Unit invoke(String s) {
                SDKLoggerKt.setMinimumLogLevel(LogLevel.Verbose);
            }
        });
```

You also have the ability to change how logs are handled or swap out logging frameworks used by the SDK

```kotlin
registerLoggerBridge(SDKLoggerBridge(
            exceptionLogger = { level, tag, message, throwable ->
                Log.println(level.code, tag, "$message\n${Log.getStackTraceString(throwable)}")
            },
            logger = { level, tag, message ->
                Log.println(level.code, tag, "$message")
            }
        ))
```

use `registerLoggerBridge` to supply a `SDKLoggerBridge` object the lambda functions supplied will handle all further logging calls

## Common Errors

> ❗️
>
> Failed to initialize the Engagement SDK. \[client-id] is not a valid client id.

If you've received this error when trying to initialize the Engagement SDK, please ensure that the Client ID used in your application matches the one given in the [Producer Suite](https://producer.livelikecdn.com/).

> ❗️ “\[program-id] is not a valid program ID”

If you've received this error, please refer back to [program ID instructions](https://livelike.readme.io/docs/android-basic-integration#section-start-a-content-session).

## Dependency Conflicts

Try to follow the same dependency version we are using in the SDK

```text
// App dependencies
constraintLayoutVersion = "1.1.3"
exoplayerVersion = "2.9.3"
glideVersion = '4.9.0'
gsonVersion = '2.8.5'
lottieVersion = '2.7.0'
mavenPluginVersion = '2.1'
multidexVersion = '1.0.3'
mixpanelVersion = '5.5.2'
okhttpVersion = '3.11.0'
pubnubVersion = '4.21.0'
supportLibraryVersion = '28.0.0'
sendbirdVersion = '3.0.88'
threetenabpVersion = "1.1.2"
lifecycleVersion = "1.1.1"
```
