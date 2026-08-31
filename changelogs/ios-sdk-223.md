---
title: iOS SDK 2.23
author: jelzon monzon
hidden: false
published_at: '2021-05-05T01:14:31.084Z'
---
## Whats New?

* Adds new factory method for creating a ContentSession that has a result completion for easier success and error handling
* Adds support for receiving custom messages

```swift
let sdk = EngagementSDK
let config = SessionConfiguration(programID: "<program-id>")

sdk.createContentSession(config) { result in
	switch result {
    case .failure(let error):
      // handle error
    case .success(let contentSession):
    	// use ContentSession instance
}
```

## Bug Fixes

* Fixes misc. Theme issues on Cheer Meter and Image Sliders