---
title: iOS SDK 2.116.1
author: Mike M
hidden: false
published_at: '2026-08-28T14:41:44.619Z'
type: improved
---
Reduced redundant network activity during SDK initialization.&#x20;

The SDK previously made two API calls to fetch the user's profile on every app launch - it now makes one. No changes to behavior or integration required.

<br />