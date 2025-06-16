---
title: useMessageItemPopover
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
      slug: react-native-usestickerpack
      title: useStickerPack
---
The purpose of `useMessageItemPopover` is to control the presence of the popover menu, using exposed states and functions.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { popoverDetail, showPopover, hidePopover } = useMessageItemPopover({\n  messageId: <Message ID>,\n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hook Argument"
}
[/block]
#### `messageId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `popoverDetail`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[PopoverDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=PopoverDetail)",
    "0-1": "{ messageId: '', popoverType: undefined }"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `showPopover`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: (args: [PopoverDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=PopoverDetail)) => void"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `hidePopover`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: `() => void`"
  },
  "cols": 1,
  "rows": 1
}
[/block]