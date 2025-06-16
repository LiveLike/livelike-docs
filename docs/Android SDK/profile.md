---
title: Profile
excerpt: Android Profile Interfaces.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Get Current Profile Information after successful SDK init.

```Text Kotlin
sdk.profile().profileStream.latest()?.let {logDebug { "profileID - ${it.id}" }}
```

In case you expect some changes in profile from other platforms like nickname, you can use getCurrentUserDetails which makes API call to get latest from backend.

```Text Kotlin
sdk.profile().getCurrentUserDetails { result, error ->
                result?.let {
                    Toast.makeText(
                        applicationContext,
                        "User:$it",
                        Toast.LENGTH_SHORT
                    ).show()
                }
                error?.let {
                    Toast.makeText(
                        applicationContext,
                        it,
                        Toast.LENGTH_SHORT
                    ).show()
                }
            }
```