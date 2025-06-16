---
title: useLoadStickerPacksEffect
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
The purpose of `useLoadStickerPacksEffect` hook is to fetch and update the sticker pack resource.

##### Example Usage: 
[block:code]
{
  "codes": [
    {
      "code": "const { reactionPacks } = useReactionPacks({\n  reactionSpaceId: \"<Reaction space ID>\",\n});\nuseLoadStickerPacksEffect();\n",
      "language": "typescript"
    }
  ]
}
[/block]