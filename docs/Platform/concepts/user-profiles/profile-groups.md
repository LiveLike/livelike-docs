---
title: Profile Groups
excerpt: Organize profiles into addressable groups
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Profile Groups is an API-first service that enables products to group profiles into named sets, allowing you to easily address groups of profiles inside of an integration. As a product developer using the Profile Groups API, you will be able to:

* Group members into flexible, dynamic sets
* Manage and query the groups a profile belongs to
* Access and list all available profile groups
* Retrieve and manage group members efficiently
* Automatically segment users based on profile attributes or activity

# Profile Groups Basics

A Profile Group can be thought of as a named set of profiles. When a profile group is first created it has no member profiles.

* The **Name** and **Description** help you organize your groups inside of the CMS, and can be used as labels inside of your integration.
* The **Members** field is the set of profiles that are part of this group.
* The **ID** is the LiveLike-assigned unique identifier of the group. It's one of the main ways to reference the group in your integration code.
* The **Custom ID** is optional but can also be used to reference the group in your integration code. A group's custom ID must be unique in your application.
* The **Attributes** are an array of key-value pairs that can be used to organize and query groups inside of  the integration. Groups are indexed by their attributes, and groups can be looked up by their attribute values.

# Types of User Groups

A Profile group supports two types of user group creation:

1. Static Profile Groups: Static groups are manually managed groups where profiles are explicitly added or removed through APIs or CMS actions. These are useful for curated audiences such as:
   1. VIP users
   2. Beta testers
   3. Premium subscribers
   4. Moderation watchlists
2. Dynamic Profile Groups: Dynamic groups automatically maintain membership based on predefined rules which can be created as per user attributes & events. Profiles are automatically added or removed at a batch interval as they match the configured criteria. These are useful for Highly engaged users, Users active during a specific event, Fans of a specific team or topic.
   1. Dynamic User Groups provide a curated list of platform controlled attributes, categories including major LiveLike features like Quests, Comments, Reactions, Streaks, Tiers, etc.
   2. Clients can also configure certain metrics from their end and update those as custom attributes on profiles and have them added to the list of attributes to make use of our user segmentation engine.
   3. Each attribute also exposes a list of supported operators for it, maintaining valid combinations and keeping rule creation as intuitive as possible.
   4. Within a single bucket of rules, rules are combined with OR logic and every new bucket that is introduced acts like an AND connection between the OR buckets.
   5. Example: Users with >10 comments in 7 days or Users who reacted to a poll or Users with toxicity score > threshold Users inactive for 30 days, “Users who have completed 5+ quests AND haven’t commented in 30 days”: re-engage active users who aren’t socializing
      <br />

> 📘 Custom IDs and attributes make data-level integrations easier
>
> Check out [Data Integration Patterns](doc:data-integration-patterns) for more ideas on using custom IDs and attributes to organize your profile groups.

# Working with Profile Groups

## Creating a new profile group

Creating a group is done via the REST API interface

```http
POST /api/v1/applications/{client_id}/profile-groups/ HTTP/1.1

Authorization: Bearer {access-token}
Content-Type: application/json

{
    "name": "Group1",
    "is_active": true,
    "description": "Sample Profile Group",
    "attributes": [
        {
            "key": "key1",
            "value": "val1"
        }
    ]
}

```

```http Response
{
    "id": "13a1fd98-24ca-4935-8791-5556586c0005",
    "name": "Group1",
    "is_active": true,
    "description": "Sample Profile Group",
    "profile_count": 0,
    "custom_id": null,
    "created_at": "2025-04-28T12:16:49.670053Z",
    "attributes": [
        {
            "key": "key1",
            "value": "val1"
        }
    ]
}
```

## Creating a new dynamic profile group

```http
POST /api/v1/applications/{client_id}/profile-groups/ HTTP/1.1

Authorization: Bearer {access-token}
Content-Type: application/json

{
    "name": "Group1",,
    "description": "Sample Profile Group",
    "attributes": [
        {
            "key": "key1",
            "value": "val1"
        }
    ],
    "membership_type": "dynamic",
    "rule_tree": {
                  "children": [
                     {
                      "children": [
                         {
                          "value": 32,
                          "attribute": "total_comments_posted",
                          "condition": "greater_than"
                         },
                         {
                          "value": true,
                          "attribute": "has_ever_commented",
                          "condition": "is"
                         }
                      ],
                      "operator": "OR"
                    }
                   ],
                  "operator": "AND"
                 },
}

```

<br />

## Listing profile groups in an app

Retrieving all the Groups for a given client's id is done via the REST API interface

```http
GET /api/v1/applications/{client-id}/profile-groups/ HTTP/1.1

Authorization: Bearer {access-token}

```

```http Response
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": "13a1fd98-24ca-4935-8791-5556586c0005",
            "name": "Group1",
            "is_active": true,
            "description": "Sample Profile Group",
            "profile_count": 0,
            "custom_id": null,
            "created_at": "2025-04-28T12:16:49.670053Z",
            "attributes": [ 
                {
                    "key": "key1",
                    "value": "val1"
                }
             ]
        }
    ]
}
```

<br />

## Updating a profile group's details

```http
PATCH /api/v1/applications/{client_id}/profile-groups/{group-id}/ HTTP/1.1

Authorization: Bearer {access-token}
Content-Type: application/json

{
    "name": "Group - edited",
    "is_active": true
}

```

**Note**: Changing **is_active** to false will make the group unavailable through the API and cause 404 on consecutive calls.

```http Response
{
    "id": "13a1fd98-24ca-4935-8791-5556586c0005",
    "name": "Group - edited",
    "is_active": true,
    "description": "Sample Profile Group",
    "profile_count": 0,
    "custom_id": null,
    "created_at": "2025-04-28T12:16:49.670053Z",
    "attributes": [ 
        {
            "key": "key1",
            "value": "val1"
        }
    ]
}
```

<br />

## Deleting a profile group

```http
DELETE /api/v1/applications/{client_id}/profile-groups/{group-id} HTTP/1.1

Authorization: Bearer {access-token}
Content-Type: application/json

```

On successful deletion of a resource, a REST API typically returns an **HTTP 204** No Content status, indicating the operation succeeded without returning a response body.

<br />

## Adding members to a profile group

Adding a member to a group is done via the REST API interface

```http
POST /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

{
    "profile_ids": [
     	 "174cc6dd-c1da-42d2-886e-c48b2bf803a8"
    ]
}

```

```http Response
{
    "successfully_added": [
        "174cc6dd-c1da-42d2-886e-c48b2bf803a8"
    ],
    "already_added": [],
    "invalid_ids": []
}
```

**Note**: Or alternatively, we can use custom_id list, but not both on the same time.

```http
POST /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

{
    "custom_ids": [
     	 "111bb1aa-c1da-42d2-886e-c48b2bf803a8"
    ]
}

```

Bulk adding a member to a group is done via the REST API interface

```http
POST /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

{
    "profile_ids": [
        "174cc6dd-c1da-42d2-886e-c48b2bf803a8",
        "d4b24ed2-f242-4a5a-9ae1-d9b7834f5a98"
    ]
}

```

**Note**: Or alternatively, we can use custom_id list, but not both on the same time.

<br />

## Removing members from a profile group

Removing a member from a group is done via the REST API interface

```http
DELETE /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

{
    "profile_ids": [
        "174cc6dd-c1da-42d2-886e-c48b2bf803a8",
        "d4b24ed2-f242-4a5a-9ae1-d9b7834f5a98"
    ]
}
```

**Note**: Or alternatively, we can use custom_id list, but not both on the same time.

```http
DELETE /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

{
    "custom_ids": [
        "111bb1aa-c1da-42d2-886e-c48b2bf803a8"
    ]
}
```

On successful deletion of a resource, a RESTful API typically returns an **HTTP 204** No Content status, indicating the operation succeeded without returning a response body.

<br />

## Listing groups a profile is a member of

Retrieving all groups for a given Profile's UUID where that profile belongs is done via the REST API interface

```http
GET /api/v1/applications/{client-id}/profiles/{profile-id}/profile-groups/ HTTP/1.1

Authorization: Bearer {access-token}

```

```http Response
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "group_id": "13a1fd98-24ca-4935-8791-5556586c0005",
            "group_name": "Group - edited",
            "profile_count": 1,
            "is_active": true,
            "created_at": "2025-04-28T12:16:49.670053Z",
            "custom_id": null
        }
    ]
}
```

<br />

## Listing profile group members

Retrieving all Profile members for a given Group's UUID done via the REST API interface

```http
GET /api/v1/applications/{client-id}/profile-groups/{group-id}/members/ HTTP/1.1

Authorization: Bearer {access-token}

```

```http Response
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": "174cc6dd-c1da-42d2-886e-c48b2bf803a8",
            "nickname": "Final Horse",
            "custom_id": null,
            "membership_created_at": "2025-04-28T12:26:43.767378Z"
        }
    ]
}
```
