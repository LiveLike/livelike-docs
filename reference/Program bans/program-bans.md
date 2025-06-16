---
title: Program Bans
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
Program Bans allow integrators to restrict certain end-users from participating in certain programs. 

This would entail restrictions on creating and publishing widgets such as text-polls, image-polls, predictions, cheer-meters etc.

## Using Program Bans:

Program Bans consist of three APIs : 

1. Create a Program Ban
2. Delete a Program Ban
3. View Program Bans

These APIs require relevant RBAC permissions on the calling profile to perform these action : 

1. create-program-ban
2. delete-program-ban
3. view-program-ban

<br>

> 📘 These permissions are also a part of the `program-moderator` role template offered by Livelike.  
> Using producer tokens would bypass these permission checks