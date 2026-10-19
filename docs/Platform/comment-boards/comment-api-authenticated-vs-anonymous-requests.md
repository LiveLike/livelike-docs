---
title: 'Comments  Authenticated vs Anonymous '
deprecated: false
hidden: true
metadata:
  robots: index
---
The comment list and detail APIs support both authenticated and anonymous requests. Authentication affects caching and personalization, but the response structure stays the same.

## Authenticated requests

When an authentication token is provided, the response is never cached and is personalized for the current viewer:

- **Reactions:** `reactions[].self_reacted_user_reaction_id` contains the viewer's reaction ID, where applicable.
- **Blocked authors:** Comments from blocked authors are excluded. Blocking applies in either direction.
- **Mentions:** Mentions of blocked profiles are removed from `mentions[]`. Blocking applies in either direction.

## Anonymous requests

When no authentication token is provided:

- Responses can be served from cache, providing significantly faster response times than authenticated requests.
- Responses are not personalized: viewer-specific reaction IDs are null, and viewer-specific blocking rules are not applied.

## Consistent response structure

No fields are added or removed based on authentication. Only field values and returned content differ, so clients can use the same response model for both modes.

For example, `self_reacted_user_reaction_id` is present in both responses but is null for anonymous requests.

If `self_reported_comment_id` is introduced in the future, it would follow the same pattern: the field would contain the current viewer's report ID where applicable and would be null for anonymous requests.

## Choosing a request mode

- Use authenticated requests when the experience depends on viewer-specific reactions and blocking rules.
- Use anonymous requests when faster responses and lower metered usage are more important than personalization.