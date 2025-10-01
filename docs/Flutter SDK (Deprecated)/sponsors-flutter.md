---
title: Sponsors (Flutter)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Sponsor API | Flutter SDK | LiveLike Developer Hub
  description: >-
    To get the list of sponsors associated with a program, you have to make a
    sponsor client and get a list of sponsors. Learn more.
  robots: index
next:
  description: ''
---
To get the list of sponsors associated with a program, you have to make a sponsor client and then\
fetch a list of sponsors by passing program id as a param like mentioned below:

```text Flutter
final sponsorsList =await sdk.sponsor.fetchByProgramId(<program-id>)
```