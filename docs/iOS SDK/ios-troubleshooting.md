---
title: Troubleshooting
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Troubleshooting | iOS SDK | LiveLike Developer Hub
  description: >-
    The iOS Engagement SDK gives you control over the types of logs that are
    prints. Learn more about iOS troubleshooting.
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

```swift
EngagementSDK.logLevel = .verbose
```

## Common Errors

> ❗️
>
> Failed to initialize the Engagement SDK. \[client-id] is not a valid client id.

If you've received this error when trying to initialize the Engagement SDK, please ensure that the Client ID used in your application matches the one given in the [Producer Suite](https://producer.livelikecdn.com/).

> ❗️ “\[program-id] is not a valid program ID”

If you've received this error, please refer back to [program ID instructions](https://livelike.readme.io/docs/ios-basic-integration#section-start-a-content-session).

## Dependency Conflicts

EngagementSDK relies on some third party and open source dependencies. The specific dependencies and supported versions can be found in the corresponding [podspec](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/EngagementSDK.podspec) and [cartfile](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Cartfile). If your application uses any of the listed dependencies, both Carthage and CocoaPods will attempt to resolve any conflict automatically by using latest version that satisfies all constraints.

We do recognize that there may be situations where this is not possible. LiveLike will make efforts to support the latest versions of all the listed dependencies. If, however, you encounter a situation where dependency conflict resolution is not automatic, please feel free to reach out to our \[support team at [support@livelike.com](mailto:support@livelike.com).
