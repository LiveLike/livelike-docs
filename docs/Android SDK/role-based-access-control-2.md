---
title: Role Based Access Control
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: livelikerbacclient
      title: LiveLikeRBACClient
---
Read [Roles and Permissions](doc:roles-and-permissions)

# Getting Started

## Installation

> 📘 Available from SDK Version 2.97.2 onwards

Add the following to` build. gradle` to get started

```Text kotlin
dependencies {
	        implementation 'com.livelike.android-engagement-sdk:livelike-kotlin-rbac:2.97.2'
	}
```

## Initialization

Import the LiveLikeRBAC library:

```swift kotlin
import com.livelike.rbac
import com.livelike.rbac.LiveLikeRBACClient
```

Initialize a LiveLikeRBACClient:

<br />

```swift kotlin
var rbac: LiveLikeRBACClient?
sdk.rbac()
```

Manage roles and permissions via the LiveLikeRBACClient: