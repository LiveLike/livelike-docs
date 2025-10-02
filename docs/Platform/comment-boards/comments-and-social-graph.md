---
title: Comments and Social Graph
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
Use the built-in integration between [Comments](doc:cms-comments) and [Social Graph](doc:social-graph-service) to filter and count comments by authors that fans follow.

## Filter comments by author profile relationship

Use the `relationship_type` and `relationship_from_profile_id` parameters on the [List comments](ref:list-comments) endpoint to filter comments by authors matching the given relationship. For example, to find comments authored by users that example-profile-id follows:

```http
GET /api/v1/comments/?relationship_type=follow&relationship_from_profile_id=example-profile-id&comment_board_id=example-board-id
```

If the `relationship_from_profile_id` is omitted, it is assumed to be the authenticated profile:

```http
GET /api/v1/comments/?relationship_type=follow&comment_board_id=example-board-id
Authorization: Bearer {access-token}
```

The above will return comments authored by users that the authenticated user follows.

## Count comments by author profile relationship

Use the `relationship_type` and `relationship_from_profile_id` parameters to count comments by authors that match the given relationship.

```http
GET /api/v1/comments/?relationship_type=follow&relationship_from_profile_id=example-profile-id&comment_board_id=example-board-id
```

<br />
