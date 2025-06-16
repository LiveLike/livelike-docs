---
title: Localization
excerpt: >-
  This doc helps out how to achieve  localization for all the resources used by
  Android SDK
deprecated: false
hidden: false
metadata:
  title: Localization | Android SDK | LiveLike Developer Hub
  description: >-
    As an integrator, you have the ability to localize the EngagementSDK
    experiences. Learn more about Android SDK localization.
  robots: index
next:
  description: ''
---
## Localize Engagement SDK components in your app

As an integrator, you have the ability to localize the EngagementSDK experiences. All of the EngagementSDK localization files can be found in EngagementSDK.aar/res/values/values.xml.\
Please refer to the screenshot below

![1757](https://files.readme.io/9df2672-Screenshot_2020-12-16_at_5.05.41_PM.png "Screenshot 2020-12-16 at 5.05.41 PM.png")

To overwrite a translated string or to add support for a new language. add the desired EngagementSDK keys to your application's resouce strings file file. The keys and values in your application's resouce strings file will prioritize over the keys and values in the EngagementSDK resouce strings file.

For example, to replace chat input field placeholder text, override the following key and new value in your resource strings file.

```text
<string name="livelike_chat_input_hint">说些什么…</string>
```

Also, You can refer to the guidelines and process mentioned in official android docs: [https://developer.android.com/guide/topics/resources/localization](https://developer.android.com/guide/topics/resources/localization)
