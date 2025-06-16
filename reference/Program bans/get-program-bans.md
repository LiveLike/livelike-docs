---
title: Get Program Bans
excerpt: ''
api:
  file: engagement-suite.json
  operationId: get-program-bans
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> This API internally checks for RBAC permissions of the calling profile. In case the permissions are present, the programs get scoped to the role scopes of the profile. If absent, the API would return an empty list.
>
> Using Producer Tokens would bypass scoping of the programs, and would return all bans for the application