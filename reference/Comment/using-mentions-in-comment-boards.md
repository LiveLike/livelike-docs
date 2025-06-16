---
title: Using Mentions in Comment Boards
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Why integrate mentions?

Mentions allow users to tag their friends/other users in comments and is a proven way (see Instagram, Facebook, WhatsApp, Slack etc) to increase user-engagement.

## What is a mention?

A mention is essentially an object with these params :

```
1. Start index
2. End index
3. Profile id
4. Custom id
```

They are delimiters in the comment text which refer to other profiles. 

Mentions allow commenters to tag other profiles.

## How are mentions created?

There are two ways to create a mention, implicitly and explicitly. Implicit mentions are automatically created by the backend from specially formatted profile IDs in the comment text. Explicit mentions are supplied by the caller when they want to use their own formatting or custom IDs that the backend wouldn’t be able to parse.

1. **Implicit**: Using the \<@profile:{id}> tag in the comment text.
2. **Explicit**: By adding an entry into the mentions list and specifying: 
   1. Start index of the mention in the text
   2. End index of the mention in the text
   3. Profile Id or custom-id of the profile being mentioned

> 📘 Currently, the API supports explicit mentions.

## How should integrators use them when creating and displaying comments?

For displaying mentions, integrators will receive a list of start, end indices and profile id for each mention in the comment text. They can replace the text within these indices to add relevant context to mentions.

1. Ordering is important within the mentions list. It represents the ordering of actual mentions in the text.
2. In case there are conflicting/overlapping mentions (as in the start and end indices of mentions overlap), then the mention object is considered invalid, resulting in 400 Bad Request during comment creation.

> 🚧 ## The tag replacement to display text (text that the integrators want to show in replacement for the mention tag) needs to be done in the reverse order, starting from the end of the text. Since it would not break the ordering of future comments, in case of size differences between the actual and replaced text.