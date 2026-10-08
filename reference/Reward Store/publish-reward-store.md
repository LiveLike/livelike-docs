---
api:
  file: applications.json
  operationId: post_client-id-reward-stores-id-publish
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
- Needs a producer credential. The caller must be authenticated, must not be an app-user profile, and  belong to an organization.
- The caller must also be a producer of this store's application. Otherwise the response is 403.