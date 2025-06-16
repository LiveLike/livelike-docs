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
[block:api-header]
{
  "title": "Getting all relationship types in an application"
}
[/block]
All relations between profiles must fall into a predefined relationship type. These relationship types can be Queried via the client interface. 

**API Definition:** [getProfileRelationshipTypes](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileRelationshipTypes)
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileRelationshipTypes } from \"@livelike/javascript\"\n\ngetProfileRelationshipTypes().then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Querying relationships"
}
[/block]
Using the client you can query relationships by any combination of the three parameters `to profile`, `relationship type` and `from profile`

**API Definition:** [getProfileRelationships](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileRelationships)

This is an example to find who is following me
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileRelationships } from \"@livelike/javascript\"\n\ngetProfileRelationships({\n   relationshipTypeKey: \"follow\",\n   toProfileId: \"<Profile ID>\",\n }).then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]
This example is who am I following
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileRelationships } from \"@livelike/javascript\"\n\ngetProfileRelationships({\n   relationshipTypeKey: \"follow\",\n   fromProfileId: \"<Profile ID>\",\n }).then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Managing relationships"
}
[/block]
Creating relationships is done one at a time via the client interface

**API Definition:** [createProfileRelationship](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=createProfileRelationship)
[block:code]
{
  "codes": [
    {
      "code": "import { createProfileRelationship } from \"@livelike/javascript\"\n\ncreateProfileRelationship({\n   relationshipTypeKey: \"follow\",\n   toProfileId: \"<Profile ID>\",\n   fromProfileId: \"<Profile ID>\",\n }).then((profileRelationship) => console.log(profileRelationship))",
      "language": "javascript"
    }
  ]
}
[/block]
Deleting relationships is similarly achieved via the client interface

**API Definition:** [deleteProfileRelationship](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=deleteProfileRelationship)
[block:code]
{
  "codes": [
    {
      "code": "import { deleteProfileRelationship } from \"@livelike/javascript\"\n\ndeleteProfileRelationship({ relationshipId: \"<Profile Relationship ID>\" })",
      "language": "javascript"
    }
  ]
}
[/block]