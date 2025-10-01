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

## List of Reaction Pack

This method is used to get list of reaction pack created through producer suite.\
It returns a Promise that resolves in paginated list of reaction pack objects.

```javascript
import { getReactionPacks } from '@livelike/javascript'

getReactionPacks().then(({results}) => console.log(results))
```

## Reaction Pack Details

This method is used to get reaction pack details using reaction pack Id.

```javascript
import { getReactionPackDetail } from '@livelike/javascript'

getReactionPackDetail({
    reactionPackId: "<Reaction Pack ID>",
}).then(reactionPack => console.log(reactionPack))
```
