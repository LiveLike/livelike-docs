---
title: Android SDK 2.79
author: Shivam Verma
hidden: false
published_at: '2023-07-03T12:55:08.426Z'
---
## What's New?

* All changes are internal: All modifications have been made internally, ensuring that they do not affect the external functionality or APIs.
* Introduced the Once class: A new Once class has been implemented, allowing developers to call asynchronous methods and store the result in the cache. This enables the reusability of the same value. Additionally, support for refreshing the value has been added, giving developers the option to update the cached value when needed.
* Removed deprecated variables and methods: Deprecated variables and methods have been removed from the codebase, ensuring a cleaner and more up-to-date implementation
* Removed the LLPaginated class: The LLPaginated class has been removed, and all associated methods have been updated accordingly. This streamlines the codebase and eliminates any unnecessary or deprecated components
* Created a Real-Time Module: A new Real-Time Module has been introduced, which contains the code for the real-time feature of LiveLike. This module includes the necessary Pubnub classes to support real-time functionality.
* Made AccessTokenDelegate non-optional: The AccessTokenDelegate parameter in the constructors of LiveLikeKotlin and EngagementSDK has been made non-optional. This ensures that an access token delegate must be provided during initialization, enhancing the security and reliability of the code.