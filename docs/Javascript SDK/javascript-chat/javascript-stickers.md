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
[block:api-header]
{
  "title": "List of Sticker Pack"
}
[/block]
This method is used to get list of sticker pack created through producer suite.
It returns a Promise that resolves the paginated list of sticker pack objects.
[block:code]
{
  "codes": [
    {
      "code": "import { getStickerPacks } from '@livelike/javascript'\n\ngetStickerPacks().then(({results}) => console.log(results))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Sticker Pack details"
}
[/block]
This method is used to get sticker pack details using sticker pack Id.
[block:code]
{
  "codes": [
    {
      "code": "import { getStickerPackDetail } from '@livelike/javascript'\n\ngetStickerPackDetail({\n  stickerPackId: \"<Sticker Pack ID>\",\n}).then(stickerPack => console.log(stickerPack))",
      "language": "javascript"
    }
  ]
}
[/block]