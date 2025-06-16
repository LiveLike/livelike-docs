---
title: useStickerPicker
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
      slug: usegifpicker
      title: useGifPicker
---
The purpose of the `useStickerPicker` is to manage and track the selected sticker pack. It exposes the selected stickerPackId value and appropriate setter function.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { selectedStickerPackId, setSelectedStickerPackId } = useStickerPicker();",
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
#### `selectedStickerPackId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "Empty String"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `setSelectedStickerPackId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "`(newSelectedStickerPickerId) => void`"
  },
  "cols": 1,
  "rows": 1
}
[/block]