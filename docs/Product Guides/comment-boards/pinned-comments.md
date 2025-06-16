---
title: Pinned Comments
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
Pinned comments allow integrators to highlight important content on comment boards. This feature is particularly useful for drawing attention to crucial information without disrupting the flow of ongoing discussions.

## When to Use Pinned Comments:

- **Highlight rules and policies**: Pin guidelines or policies to ensure visibility for users.
- **Showcase classic or important posts**: Elevate noteworthy or user-submitted content.
- **Alert users to issues or unplanned events**: Keep users informed of significant updates or problems.

## Pinned Comments Basics

Pinned comments are tied to the existing comments system and subject to **roles and permissions**. Users who have specific permissions can manage pinned comments across different boards. For more details, refer to the [roles and permissions guide](https://docs.livelike.com/docs/roles-and-permissions).

- **Permissions System**: Permissions for pinning and unpinning comments are managed through the platform’s roles and permissions. Users with the **pin-comment** permission, producers or the owner of the comment board can pin or unpin comments.
- **Cascading Deletes**: If the underlying comment of a pinned comment is deleted, the pinned comment is automatically removed to maintain data consistency.

## Pinning Comments

To pin a comment, the user must have the **pin-comment** permission or be a producer or board owner. This ensures that only authorized users can perform pin actions. To implement this functionality, refer to the following API documentation:

- [Pin Comment API Documentation](https://docs.livelike.com/reference/create-a-pinned-comment)

## Un-pinning Comments

To unpin a comment, the same permissions required for pinning are necessary. Authorized users with the **pin-comment** permission, producers or board owners can unpin comments as needed. More information can be found in the API documentation:

- [Un-pin Comment API Documentation](https://docs.livelike.com/reference/unpin-a-pinned-comment)

## Listing Pinned Comments

There are two APIs available for retrieving a list of pinned comments. Depending on the context, one API may be more suitable than the other.

1. **Server-to-Server Listing (Auth Token Required)**  
   This API is designed for server-to-server communication, where an authenticated request is necessary. This is ideal for backend operations. The full details are in the documentation

- [List Pinned Comments (Auth Required) API Documentation](https://docs.livelike.com/reference/list-pinned-comments)

2. **Public Listing for Displaying Pinned Comments**  
   This API is more suitable for frontend use cases where you need to display pinned comments in the UI. No authentication token is required. Find more details here:

- [Public Listing Pinned Comments API Documentation](https://docs.livelike.com/reference/list-comment-board-pinned-comments)

## Permissions for Listing:

**pin-comment** permission is not required to simply view pinned comments, but it is necessary for pinning and un-pinning actions.