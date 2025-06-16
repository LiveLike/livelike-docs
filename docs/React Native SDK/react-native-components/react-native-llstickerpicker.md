---
title: LLStickerPicker
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
      slug: llthemeswitch
      title: LLThemeSwitch
---
`LLGifPicker` renders a Sticker picker component when a user press on sticker-picker icon in composer
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2e75341-Screenshot_2023-01-30_at_11.04.10.png",
        "Screenshot 2023-01-30 at 11.04.10.png",
        1810,
        1492,
        "#000000"
      ]
    }
  ]
}
[/block]
##### Customise styles for Stock `LLStickerPicker` component example:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLBasePickerStyles,\n  LLChat,\n  LLChatMessageComposer,\n  LLChatMessageComposerProps,\n  LLStickerPicker,\n  LLStickerPickerProps,\n  LLStickerPickerStyles,\n  useTheme,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\nimport { useMemo } from 'react';\n\nfunction MyStickerPicker(props: LLStickerPickerProps) {\n  const { themeType } = useTheme();\n  const pickerComponentStyles = useMemo(() => pickerComponentStylesFn(themeType), [themeType]);\n\n  return (\n    <LLStickerPicker\n      {...props}\n      PickerComponentStyles={pickerComponentStyles}\n      styles={gifPickerStyles}\n    />\n  );\n}\n\nfunction MyComposer(props: LLChatMessageComposerProps) {\n  return (\n    <LLChatMessageComposer\n      {...props}\n      StickerPickerComponent={MyStickerPicker}\n    />\n  );\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}\n\nconst gifPickerStyles: Partial<LLStickerPickerStyles> = StyleSheet.create({\n  pickerCloseIcon: { height: 12, width: 12 },\n  stickerImage: { width: 70, height: 70 },\n  stickerPackIcon: { height: 22, width: 22 },\n});\nconst pickerComponentStylesFn: (\n  theme: 'light' | 'dark'\n) => Partial<LLBasePickerStyles> = (theme) =>\n  StyleSheet.create({\n    pickerContainer: {\n      minHeight: 250,\n      maxHeight: 350,\n      backgroundColor: theme === 'light' ? '#A0C3D2' : '#2b4956',\n    },\n    pickerItemsScrollview: {\n      padding: 10,\n    },\n  });",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLStickerPicker"
}
[/block]
* [useStickerPacks](react-native-usestickerpacks)
* [useStickerPicker](react-native-usestickerpicker)
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLStickerPicker Props"
}
[/block]
#### `visible`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "boolean",
    "0-1": "false if not present"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `closeStickerPicker`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Function of type: `() => void`"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `onSelectSticker`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: `(stickerShortcode: string) => void` (**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `PickerComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLBasePicker` styles.",
    "0-0": "[LLBasePickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLBasePickerStyles)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `styles`
[block:parameters]
{
  "data": {
    "0-0": "StyleSheet of type [LLStickerPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPickerStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLStickerPicker` styles."
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### Styles Props
[block:parameters]
{
  "data": {
    "h-0": "CSS Class",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "stickerPacksContainer",
    "1-0": "stickerImageContainer",
    "2-0": "stickerHeaderContainer",
    "4-0": "stickerImage",
    "3-0": "stickerPackIcon",
    "5-0": "pickerCloseIcon",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "2-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "3-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "4-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "5-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Sticker packs item container",
    "1-2": "Sticker item container",
    "2-2": "Root sticker packs container",
    "3-2": "Sticker packs item styles",
    "4-2": "Sticker item styles",
    "5-2": "Sticker picker close icon styles"
  },
  "cols": 3,
  "rows": 6
}
[/block]