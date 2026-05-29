---
api:
  file: applications.json
  operationId: patch_client-id-reward-multipliers-reward-multiplier-id
hidden: true
link:
  new_tab: false
metadata:
  robots: noindex
---
# Update Streak

A streak can be fully updated while it is in the **draft** state, allowing modification of all configuration fields before publication.

Once a streak is **published**, only a limited set of fields can be updated to preserve configuration integrity. The following fields remain editable after publication:

- `name`
- `description`
- `starts_at`
- `expires_at`
- `attributes`

All other fields become immutable after the streak is published.
