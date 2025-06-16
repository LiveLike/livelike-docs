---
title: Stickers
excerpt: >-
  Stickers are images or animations that can be used inside of chat messages.
  They can be customized to match an app's look and feel.
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
      slug: javascript-reactions
      title: Reactions
---
## List of Sticker Pack

This method is used to get list of sticker pack created through producer suite.\
It returns a Promise that resolves the paginated list of sticker pack objects.

```javascript
import { getStickerPacks } from '@livelike/javascript'

getStickerPacks().then(({results}) => console.log(results))
```

## Sticker Pack details

This method is used to get sticker pack details using sticker pack Id.

```javascript
import { getStickerPackDetail } from '@livelike/javascript'

getStickerPackDetail({
  stickerPackId: "<Sticker Pack ID>",
}).then(stickerPack => console.log(stickerPack))
```
