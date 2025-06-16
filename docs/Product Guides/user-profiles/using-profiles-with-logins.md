---
title: Integrating with Logins
excerpt: Connect and extend your existing user accounts and logins with Profiles
deprecated: false
hidden: false
metadata:
  title: Using Profiles with Logins | LiveLike Developer Hub
  description: >-
    Profiles are used to accumulate points, virtual goods, and interaction
    history for users. Learn more about integrating with logins.
  robots: index
next:
  description: >-
    Read more about Profiles, and how to integrate them on your platform with
    the LiveLike SDKs.
  pages:
    - type: basic
      slug: web-user-profile-integration
      title: User Profile Integration
    - type: basic
      slug: custom-profile-ids
      title: Custom Profile IDs
---
..Profiles are used to accumulate points, virtual goods, and interaction history for users. Profiles are meant to enhance your existing user records if you already have them, but they can also be used independently. For a higher-level view of what profiles do and how they work, read more about them in the [profiles section of the product guide](doc:user-profiles).

This guide assumes your project already has user logins, and want to extend them with things like points and leaderboards, or the ability to join chats. Connecting user accounts with LiveLike profiles enables a persistent experience where interaction histories, reward balances, and preferences carry over between sessions.

## Obtain a Profile

There are two ways to obtain a profile:

1. Client-side, using one of the SDKs.
2. Server-side, [using the REST API](ref:using-profiles-api).

Once you have a profile instance, you can do things like change its display name and have it join chats. When a profile is created, it includes an <Glossary>Access Token</Glossary>. This works like a credential, and is what your app needs to save to re-use the profile associated with it. Try to keep it a secret, because anyone who has that access token can use it to modify the profile.

> 📘 Want to use your own user IDs?
>
> You can associate your own IDs with profiles by using [Custom Profile IDs](doc:custom-profile-ids).

## Associate the Profile with a User

If you know which user to associate the profile with, you should store the access token on your user record. Here are some common scenarios:

* A logged-in user enters a section of the app that has chat or widgets for the first time. Their user account doesn't have a LiveLike access token already stored on it, so a new profile is created with the LiveLike SDK. You then store the access token in the logged-in user's account records.
* A new user signs up in your app. Your backend calls the LiveLike API to create the profile, and stores the profile access token on the new user record.

<Image title="Login Integration.png" alt={630} align="center" src="https://files.readme.io/cc74a91-Login_Integration.png">
  An existing user logging in to an app with the LiveLike SDK integrated.
</Image>

Now going forward, the LiveLike SDK's should be initialized with that access token. The user associated with that profile will now continue to earn points, gain ranks on the leaderboard, and everything else that the LiveLike SDK allows. Storing the profile access token on the user record allows progress to be saved across installs, devices, and platforms.

## Handling Logged-out vs. Logged-in

Profiles work independently of your login system, so any points that a user earns while logged out can be kept after they sign up or log in! This is common for sophisticated on-boarding where users can try things out before signing up.

A profile can be created before a user login is available, and then kept in session storage. When the user does finally convert, remember to pass along the profile access token so that the signup process can store it on your user record. Then in the future, when that user logs in again, their stored access token can be passed back into the SDK so that the same profile is re-used.

## Retrieving Current Profile Id

Once your user is associated with a profile your application may need the profile Id to complete other tasks within the LiveLike systems. 

```kotlin
sdk.getCurrentUserDetails(object :
	LiveLikeCallback<LiveLikeUserApi>() {
		override fun onResponse(result: LiveLikeUserApi?, error: String?) {
			result?.let {
				Toast.makeText(
					applicationContext,
					"Profile Id: ${it.userId}",
					Toast.LENGTH_SHORT
				).show()
			}
		}
	})
```
```Text Swift
sdk.getCurrentUserProfileID { result in
    switch result {
    case .success(let id):
        self.currentProfileID.text = id
    case .failure(let error):
        self.showAlert(title: "Error", message: error.localizedDescription)
    }
}
```
