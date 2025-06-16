---
title: Reactions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: javascript-reaction-pack
      title: Reaction Pack
    - type: basic
      slug: javascript-reaction-space
      title: Reaction Space
    - type: basic
      slug: javascript-user-reaction
      title: User Reaction
---
Use Reactions based API, if you need your content to be reacted by your application users based on your custom reactions. For example:
1. User reaction on a video moment for a video stream being played
2. User reaction on blog post comments
3. User reaction on chat room messages
[block:api-header]
{
  "title": "Basic reaction workflow:"
}
[/block]
A basic reaction workflow involves:
1. Creating a reaction pack through producer suite.
2. Creating reaction space using reaction pack Ids along with unique identifier of your content entity (termed as target group Id) which forms a collection of items, for example:
      a. In a video application, target group Id could be a "Video Id" which has a collection of video moments.
      b. In a blog post application, target group Id could be a "Blog post Id" which has a collection of blog post comments.
      c. In a chat application, target group Id could be a "Chat room Id" which has a collection of chat messages
3. Add or remove reactions on a given item using:
      a. Item unique identifier (termed as target Id)
      b. Reaction space id
      c. Reaction Id of reaction icon which is part of reaction pack created in step 1 where the id of this reaction pack was also used to create a reaction space.
[block:api-header]
{
  "title": "Components of Reaction based API"
}
[/block]
1. Reaction Pack API - Used to manage Reaction packs in a given application 
2. Reaction Space API - Used to manage Reaction space created for a given target group
3. User Reaction API - Used to manage user reactions