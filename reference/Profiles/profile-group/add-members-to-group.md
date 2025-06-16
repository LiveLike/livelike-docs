---
title: Add Members to Group
excerpt: ''
api:
  file: engagement-suite.json
  operationId: add-members-to-group
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Add one of the following parameters:

- custom_ids: A list of custom ID strings for application profiles that have already been created.
- profile_ids: A list of application profile IDs for application profiles that have already been created.  
  These application profiles will be added as members of the group.

A profile can belong to multiple groups. Duplicate profile or custom IDs will be ignored, ensuring each profile is added only once as a member.

While adding members to a group, if a custom ID or profile ID is invalid or already a member of the group, it will be included in the corresponding key in the response.