---
title: Reaction Pack
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
      slug: javascript-reaction-space
      title: Reaction Space
---
Reaction pack resource lets you create and manage your custom reaction icons through producer suite. Once reaction pack is created, you may get list of reaction packs and reaction pack details.
[block:api-header]
{
  "title": "List of Reaction Pack"
}
[/block]
This method is used to get list of reaction pack created through producer suite.
It returns a Promise that resolves in paginated list of reaction pack objects.
[block:code]
{
  "codes": [
    {
      "code": "import { getReactionPacks } from '@livelike/javascript'\n\ngetReactionPacks().then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Reaction Pack Details"
}
[/block]
This method is used to get reaction pack details using reaction pack Id.
[block:code]
{
  "codes": [
    {
      "code": "import { getReactionPackDetail } from '@livelike/javascript'\n\ngetReactionPackDetail({\n    reactionPackId: \"<Reaction Pack ID>\",\n}).then(reactionPack => console.log(reactionPack))",
      "language": "javascript"
    }
  ]
}
[/block]