---
title: Android SDK 3.0.26
author: Viktor Manev
hidden: true
published_at: '2026-11-03T13:32:23.576Z'
type: improved
---
## Profile Loading Improvements

- Improved handling of profile-loading failures
- Prevented requests with missing profile IDs

## Fixes

- Fixed profile-loading failures to prevent requests with missing profile IDs
- `currentProfileOnce()` now throws on loading failure or a missing profile ID

## New Features

- Added `getCurrentProfileOrNull()` to safely retrieve a profile, returning `null` on error