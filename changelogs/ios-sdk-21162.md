---
title: iOS SDK 2.116.2
author: LJupcho Nastevski
hidden: false
published_at: '2026-09-02T12:48:33.224Z'
type: improved
---
Reduced redundant network activity during SDK initialization.

The SDK previously made two API calls to fetch the application configuration every app launch - it now makes one. No changes to behavior or integration required.