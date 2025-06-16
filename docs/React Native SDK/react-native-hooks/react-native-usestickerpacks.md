---
title: useStickerPacks
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
      slug: useloadstickerpackseffect
      title: useLoadStickerPacksEffect
---
The purpose of `useStickerPacks` hook is to expose sticker packs resource.

##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "const { stickerPacks } = useStickerPacks();",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `stickerPacks`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Array of items of type: [IStickerPack](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IStickerPack)",
    "0-1": "Empty Array"
  },
  "cols": 2,
  "rows": 1
}
[/block]