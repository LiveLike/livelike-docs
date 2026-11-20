---
title: Android SDK 3.0.28
author: Viktor Manev
hidden: false
published_at: '2026-11-20T17:01:05.396Z'
---
## Changes

- Added `sdk.setGetRequestInterceptor()` to customize outgoing LiveLike API GET requests, including per-request authentication control.
- Deprecated `preferAnonymousRequests` in favor of the new interceptor.
- Fixed duplicate query parameters in comment-count and comment-related pagination requests.
- Added versioned Android SDK API reference documentation. <br />[https://sdk-reference.livelikecdn.com/android](https://sdk-reference.livelikecdn.com/android "https://sdk-reference.livelikecdn.com/android")

## Example: Removing authentication from comment requests

```kotlin
import com.livelike.network.removeAuth
import io.ktor.http.encodedPath

sdk.setGetRequestInterceptor { request ->
    if (request.url.encodedPath == "/api/v1/comments/") {
        request.headers.removeAuth()
    }
}
```

This example removes authentication from comment GET requests. The interceptor applies only to HTTPS GET requests to `cf-blast.livelikecdn.com`.

## Removing the interceptor

Pass `null` to remove it:

```kotlin
sdk.setGetRequestInterceptor(null)
```