---
title: Create A Flair Assignment
excerpt: >-
  If scope id and resource kind are not defined flair is assigned globally to
  the profile.
api:
  file: engagement-suite.json
  operationId: post_flair-assignments
deprecated: false
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
If you want to add scope by resource kind just pass resource kind. If you want specific scope with resource id you must pass resource kind and resource id. If scope id is in request resource kind and resource id will be ignored
