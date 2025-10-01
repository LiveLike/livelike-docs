---
title: Social Graph
excerpt: >-
  Define relationships between users and use them to personalize their
  experience
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Social Graph is an API-first service that enables products to define and explore the social connections between their users and then use those relationships to personalize features. As a product developer using the Social Graph service, you will be able to:

* Create and query connections between your users
* Define your own relationship types like followers, friends, classmates, or anything else
* Discover and analyze connections in your network of users
* Integrate with your existing features and user data

## Getting all relationship types in an application

All relations between profiles must fall into a predefined relationship type. These relationship types can be Queried via the client interface. 

**API Definition:** [getProfileRelationshipTypes](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileRelationshipTypes)

```javascript
import { getProfileRelationshipTypes } from "@livelike/javascript"

getProfileRelationshipTypes().then(({results}) => console.log(results))
```

## Querying relationships

Using the client you can query relationships by any combination of the three parameters `to profile`, `relationship type` and `from profile`

**API Definition:** [getProfileRelationships](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileRelationships)

This is an example to find who is following me

```javascript
import { getProfileRelationships } from "@livelike/javascript"

getProfileRelationships({
   relationshipTypeKey: "follow",
   toProfileId: "<Profile ID>",
 }).then(({results}) => console.log(results))
```

This example is who am I following

```javascript
import { getProfileRelationships } from "@livelike/javascript"

getProfileRelationships({
   relationshipTypeKey: "follow",
   fromProfileId: "<Profile ID>",
 }).then(({results}) => console.log(results))
```

## Managing relationships

Creating relationships is done one at a time via the client interface

**API Definition:** [createProfileRelationship](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createProfileRelationship)

```javascript
import { createProfileRelationship } from "@livelike/javascript"

createProfileRelationship({
   relationshipTypeKey: "follow",
   toProfileId: "<Profile ID>",
   fromProfileId: "<Profile ID>",
 }).then((profileRelationship) => console.log(profileRelationship))
```

Deleting relationships is similarly achieved via the client interface

**API Definition:** [deleteProfileRelationship](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteProfileRelationship)

```javascript
import { deleteProfileRelationship } from "@livelike/javascript"

deleteProfileRelationship({ relationshipId: "<Profile Relationship ID>" })
```
