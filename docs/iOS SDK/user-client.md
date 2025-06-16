---
title: User Client
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
User Client is an interface that can be used for features related to users applicable across an application.

**Features**

* Block a User Profile
* Unblock a User Profile
* Get List of User Profiles that have been blocked

## Block Profile

As an integrator, you can now allow users to block other users from sending invitations or adding them to chat rooms.

To enable the user to block other users, you can implement the `blockProfile` method which is a part of the `ChatClient`. It accepts a parameter `profileID` which corresponds to the id of the profile to be blocked.

On successful completion, the method returns an object of type `BlockInfo` which contains details of the profile blocked and the profile it was blocked by.

```swift
sdk.user.blockProfile(
		profileID: profileID
) { result in
   	switch result {
    case .success(let blockedProfile):
         self.showAlert(
            title: "Profile Blocked",
         		message: "Id:\(blockedProfile.blockedProfileID)"
         )
    case .failure(let error):
    		self.showAlert(title: "Error", message: error.localizedDescription)
		}
}
```

## Unblock profile

As an integrator, you can now allow users to unblock users they had previously blocked from sending invitations or adding them to chat rooms.

To enable the user to unblock other users, you can implement the `unblockProfile` method which is a part of the `ChatClient`. It accepts one parameter: `blockRequestID` which corresponds to the id of the  `BlockInfo` for the blocked profile.

```swift
sdk.user.unblockProfile(blockRequestID: requestID) { result in
		switch result {
    case .success(_):
    		break
    case .failure(let error):
    		self.showAlert(title: "Error", message: error.localizedDescription)
		}
}
```

## Get List of Blocked Profiles

As an integrator, you can show the user a list of all the profiles blocked by the user.

To display the list, you can implement the `getBlockedProfileList` method which is a part of the `ChatClient`. The method accepts a parameter `profileID` which corresponds to the id of the profile blocked which can be used as a filter for the request and is `optional`.

On successful completion, the method returns a paginated list of type `BlockInfo` which contains details of the profile blocked and the profile it was blocked by.

```swift
sdk.user.getBlockedProfileList(
		blockedProfileID: profileID, 
		page: .first
) { result in
            switch result {
		case .success(let blockedProfiles):
				if blockedProfiles.count >= 1 {
						self.showAlert(
            		title: "No. of Profiles:",
                message: "\(blockedProfiles.count)"
        		)
    		}
		case .failure(let error):
    		print(error.localizedDescription)
		}
}
```
