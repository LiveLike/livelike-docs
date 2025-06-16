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
[block:api-header]
{
  "type": "basic",
  "title": "Logging & Debugging"
}
[/block]
The Engagement SDK gives you control over the types of logs that are printed. This can be helpful to debug unexpected behavior or for reporting a bug to [support@livelike.com](mailto:support@livelike.com). The different logging levels are:

* **Verbose** - Highly detailed level of logging, best used when trying to understand the working of a specific section/feature of the Engagement SDK.
* **Debug** - Information that is diagnostically helpful to integrators and Engagement SDK developers.
* **Info** - Information that is always useful to have, but not vital.
* **Warning** - Information related to events that could potentially cause oddities, but the Engagement SDK will continue working as expected.
* **Error** - An error occurred that is fatal to a specific operation/component, but not the overall Engagement SDK.
* **Severe** - A fatal issue occurred, from which the Engagement SDK cannot recover.
* **None** - No logging enabled.

The default level is **None**.
[block:code]
{
  "codes": [
    {
      "code": "SDKLogger.minimumLogLevel = LogLevel.Verbose",
      "language": "kotlin"
    },
    {
      "code": "SDKLoggerKt.setMinimumLogLevel(LogLevel.Verbose);",
      "language": "java"
    }
  ]
}
[/block]
You also have the ability to add your own listener for the logs.
[block:code]
{
  "codes": [
    {
      "code": "registerLogsHandler(object : (String) -> Unit {\n  override fun invoke(text: String) {\n    // Do something with the log here\n  }\n})",
      "language": "kotlin"
    },
    {
      "code": "        SDKLoggerKt.registerLogsHandler(new Function1<String, Unit>() {\n            @Override\n            public Unit invoke(String s) {\n                SDKLoggerKt.setMinimumLogLevel(LogLevel.Verbose);\n            }\n        });",
      "language": "java"
    }
  ]
}
[/block]
You also have the ability to change how logs are handled or swap out logging frameworks used by the SDK
[block:code]
{
  "codes": [
    {
      "code": "registerLoggerBridge(SDKLoggerBridge(\n            exceptionLogger = { level, tag, message, throwable ->\n                Log.println(level.code, tag, \"$message\\n${Log.getStackTraceString(throwable)}\")\n            },\n            logger = { level, tag, message ->\n                Log.println(level.code, tag, \"$message\")\n            }\n        ))",
      "language": "kotlin"
    }
  ]
}
[/block]
use `registerLoggerBridge` to supply a `SDKLoggerBridge` object the lambda functions supplied will handle all further logging calls
[block:api-header]
{
  "title": "Common Errors"
}
[/block]

[block:callout]
{
  "type": "danger",
  "body": "Failed to initialize the Engagement SDK. [client-id] is not a valid client id.",
  "title": ""
}
[/block]
If you've received this error when trying to initialize the Engagement SDK, please ensure that the Client ID used in your application matches the one given in the [Producer Suite](https://producer.livelikecdn.com/).
[block:callout]
{
  "type": "danger",
  "body": "“[program-id] is not a valid program ID”"
}
[/block]
If you've received this error, please refer back to [program ID instructions](https://livelike.readme.io/docs/android-basic-integration#section-start-a-content-session).
[block:api-header]
{
  "title": "Dependency Conflicts"
}
[/block]
Try to follow the same dependency version we are using in the SDK
[block:code]
{
  "codes": [
    {
      "code": "// App dependencies\nconstraintLayoutVersion = \"1.1.3\"\nexoplayerVersion = \"2.9.3\"\nglideVersion = '4.9.0'\ngsonVersion = '2.8.5'\nlottieVersion = '2.7.0'\nmavenPluginVersion = '2.1'\nmultidexVersion = '1.0.3'\nmixpanelVersion = '5.5.2'\nokhttpVersion = '3.11.0'\npubnubVersion = '4.21.0'\nsupportLibraryVersion = '28.0.0'\nsendbirdVersion = '3.0.88'\nthreetenabpVersion = \"1.1.2\"\nlifecycleVersion = \"1.1.1\"",
      "language": "text",
      "name": null
    }
  ]
}
[/block]