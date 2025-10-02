---
title: Reactions and Social Graph
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: social-graph-service
      title: Social Graph
      type: basic
---
Use the built-in integration between [Reactions](doc:reactions) and [Social Graph](doc:social-graph-service) to filter and count user reactions by others that fans follow.

## Common parameters

The `relationship_type` parameter species what kind of relationship to filter responses by. Its value should be the _relationship type key_ like `follows` belonging to the relationship type from the social graph to filter by.

The `relationship_from_profile_id` species the perspective that the filtering should be from. Its value should be the profile ID in the _from_ part of the relationship. For example, if Alice follows Bob, then the relationship is from Alice to Bob, and Alice would be the from part. If this parameter is not provided then it defaults to the authenticated user.

## Filter reactions by profile relationship

Use the `relationship_type` and `relationship_from_profile_id` parameters on the [List user reactions](ref:list-user-reactions) endpoint to filter reactions by authors matching the given relationship. For example, to find reactions from users that example-profile-id follows:

```http
GET /api/v1/user-reactions/?relationship_type=follow&relationship_from_profile_id=example-profile-id&reaction_space_id=example-space-id
```

If the `relationship_from_profile_id` is omitted, it is assumed to be the authenticated profile:

```http
GET /api/v1/user-reactions/?relationship_type=follow&reaction_space_id=example-space-id
```

The above will return reactions from users that the authenticated user follows.

## Count reactions by profile relationship

Use the `relationship_type` and `relationship_from_profile_id` parameters on the [Get user reaction count](ref:get-user-reaction-count) endpoint to count reactions from users that match the given relationship.

```http
GET /api/v1/user-reactions-count/?relationship_type=follow&relationship_from_profile_id=example-profile-id&reaction_space_id=example-space-id
```