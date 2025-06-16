---
title: Role-Based Access Control (iOS)
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
Read Product Guide [here](doc:roles-and-permissions)

# Getting Started

## Installation

> 📘 Available for SPM and Cocoapods in versions 2.94+

### Swift Package Manager

1. Open your project inside of Xcode and navigate to File > Add Packages...
2. Search for <https://bitbucket.org/livelike/livelike-ios-sdk.git> and select the livelike-ios-sdk swift package
3. Use the Up to Next Major Version dependency rule spanning from 2.0.0 \< 3.0.0, and hit the Add Package button

### CocoaPods

<https://guides.cocoapods.org/using/using-cocoapods.html>

Add the following to a Podfile:

```Text Podfile
target '<application-target-name>' do  
    use_frameworks!  
    pod 'LiveLikeRBAC'  
end
```

## Initialization

### Import the LiveLikeRBAC library:

```swift
import LiveLikeRBAC
```

### Initialize a LiveLikeRBACClient:

```swift
var rbac: LiveLikeRBACClient?

LiveLikeRBACClient.make(
    config: RBACClientConfig(
        clientID: "<client-id>",
        accessToken: "<access-token>"
    )
) { result in
   switch result {
   case .failure:
     // handle failure
   case .success(let rbac):
     self.rbac = rbac
   }
}
```

### Manage roles and permissions via the LiveLikeRBACClient

- **Roles** are assigned to profiles and permission checks are performed against the authenticated profile's roles when they are performing some action. A profile can be assigned more than one role.
- **Permissions** represent an action a user can perform, like posting a comment or deleting a board. Permissions are granted to roles, and in effect a role is a named set of permissions. Once a role is assigned to a profile, that profile has all of that role's permissions.
- **Scopes** control which resources the role assignment is effective in. A role assignment is valid for one or more scopes.
- **Resources** are the entities that profiles act upon. Resources are things like Applications, Programs, Comment Boards, Chat Rooms, Chat Room Messages, and so on.

<br />

#### Create a role assignment

[RBACRoleAssignment](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACRoleAssignment.swift)

```swift
rbac.createRoleAssignment(
    options: CreateRoleAssignmentOptions(
        roleKey: "<role-key>",
        profileID: "<profile-id>",
        resourceKind: "<kind>"
        resourceKey: "<resource-key>"
    )
) { result in
   ...
}
```

#### Delete a role assignment

[RBACRoleAssignment](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACRoleAssignment.swift) 

```swift
rbacClient.deleteRoleAssignment(
    options: DeleteRoleAssignmentOptions(
        roleAssignmentID: "<role-assignment-id>"
    )
) { result in
   ...
}
```

#### List assigned roles

[RBACRoleAssignment](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACRoleAssignment.swift)

```swift
rbacClient.getAssignedRoles(
    page: .first,
    options: ListAssignedRolesOptions(
        profileID: "<profile-id>"
    )
) { result in
   ...
}
```

#### List permission

[RBACPermission](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACPermission.swift) 

```swift
rbacClient.getPermisions(
    page: .first,
    options: ListPermissionsOptions(profileID: "<profile-id>"
) { result in
   ...
}
```

#### List roles

[RBACRole](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACRole.swift)

```swift
rbacClient.getRoles(
    page: .first,
    options: ListRolesOptions()
) { result in
   ...
}
```

#### List resources

[RBACResource](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACResource.swift) 

```swift
rbacClient.getResources(
    page: .first,
    options: ListResourceOptions()
) { result in
   ...
}
```

#### List scopes

[RBACScope](https://bitbucket.org/livelike/livelike-ios-sdk/src/master/Sources/LiveLikeRBAC/Models/RBACScope.swift) 

```swift
rbacClient.getScopes(
    page: .first,
    options: ListScopesOptions(resourceID: "<resource-id>")
) { result in
   ...
}
```