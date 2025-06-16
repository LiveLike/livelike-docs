---
title: LLGifPicker
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
      slug: react-native-llstickerpicker
      title: LLStickerPicker
---
`LLGifPicker` renders a Gif picker component when a user press on gif-picker icon in composer
The component consists of:
* `Header` - Search input and close button
* `Picker` - Gifs based on search result
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fb7da9f-Screenshot_2023-01-28_at_16.24.34.png",
        "Screenshot 2023-01-28 at 16.24.34.png",
        1916,
        1606,
        "#000000"
      ]
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "GIFs are not supported by default on Android",
  "body": "You will need to add **com.facebook.fresco:animated-gif:2.+** as an additional dependency to **android/app/build.gradle**\n[Read more...](https://reactnative.dev/docs/0.62/image#gif-and-webp-support-on-android)"
}
[/block]
##### Custom implementation for `GifPickerHeaderComponent` example:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatMessageComposer,\n  LLChatMessageComposerProps,\n  LLGifPicker,\n  LLGifPickerHeaderProps,\n  LLGifPickerProps,\n  LLGifPickerStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nfunction MyGifPickerHeader(props: LLGifPickerHeaderProps) {\n  // Render your custom gif picker header\n}\n\nfunction MyGifPicker(props: LLGifPickerProps) {\n  return (\n    <LLGifPicker\n      {...props}\n      GifPickerHeaderComponent={MyGifPickerHeader}\n    />\n  );\n}\n\nfunction MyComposer(props: LLChatMessageComposerProps) {\n  return <LLChatMessageComposer {...props} GifPickerComponent={MyGifPicker} />;\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}",
      "language": "typescript"
    }
  ]
}
[/block]
##### Customise styles for Stock `LLGifPicker`, `LLGifPickerHeader` and `LLBasePicker` component example:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLBasePickerStyles,\n  LLChat,\n  LLChatMessageComposer,\n  LLChatMessageComposerProps,\n  LLGifPicker,\n  LLGifPickerHeaderStyles,\n  LLGifPickerProps,\n  LLGifPickerStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nfunction MyGifPicker(props: LLGifPickerProps) {\n  return (\n    <LLGifPicker\n      {...props}\n      GifPickerHeaderComponentStyles={gifPickerHeaderStyles}\n      PickerComponentStyles={gifPickerComponentStyles}\n      styles={gifPickerStyles}\n    />\n  );\n}\n\nfunction MyComposer(props: LLChatMessageComposerProps) {\n  return <LLChatMessageComposer {...props} GifPickerComponent={MyGifPicker} />;\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}\n\nconst gifPickerStyles: Partial<LLGifPickerStyles> = StyleSheet.create({\n  gifImage: { height: 100, width: 100 },\n  gifImageContainer: { margin: 10 },\n});\nconst gifPickerHeaderStyles: Partial<LLGifPickerHeaderStyles> =\n  StyleSheet.create({\n    headerContainer: { padding: 5 },\n    searchInput: { borderRadius: 10, height: 50, padding: 10 },\n    closeIcon: { height: 30, width: 30 },\n  });\nconst gifPickerComponentStyles: Partial<LLBasePickerStyles> = StyleSheet.create(\n  {\n    pickerContainer: {\n      minHeight: 250,\n      maxHeight: 350,\n      backgroundColor: 'white',\n    },\n    pickerItemsScrollview: {\n      padding: 10,\n    },\n  }\n);",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLGifPicker"
}
[/block]
* [useGifPicker](react-native-usegifpicker)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLGifPicker Props"
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
#### `closeGifPicker`
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
#### `onSelectGif`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: (gifImage: [IGif](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IGif)) => void (**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `GifPickerHeaderComponent`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "React Component of type [LLGifPickerHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeader)",
    "0-1": "[`LLGifPickerHeader`](https://docs.livelike.com/docs/react-native-llgifpicker#llgifpickerheader)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `GifPickerHeaderComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLGifPickerHeader` styles.",
    "0-0": "[LLGifPickerHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeaderStyles)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `PickerComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLBasePickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLBasePickerStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLBasePicker` styles."
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `styles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "StyleSheet of type [LLGifPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLGifPicker` styles."
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
    "0-0": "gifImageContainer",
    "1-0": "gifImage",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Gif image container styles",
    "1-2": "Gif image styles"
  },
  "cols": 3,
  "rows": 2
}
[/block]

[block:api-header]
{
  "title": "LLGifPickerHeader"
}
[/block]
`LLGifPickerHeader` renders a header of the gif picker component and consists of search input and close button
[block:api-header]
{
  "title": "Hooks used by LLGifPickerHeader"
}
[/block]
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLGifPickerHeader Props"
}
[/block]
#### `onSearchInputChange`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: \n`(gifSearchInput: string, options?: { debounce: boolean;}) => void`\n(**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `closeGifPicker`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: `() => void`\n(**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `styles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLGifPickerHeader` styles.",
    "0-0": "StyleSheet of type [LLGifPickerHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeaderStyles)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### Style Props
[block:parameters]
{
  "data": {
    "h-0": "CSS Class",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "headerContainer",
    "1-0": "searchInput",
    "2-0": "closeIcon",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "2-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Root header container",
    "1-2": "Search input styles",
    "2-2": "Close icon styles"
  },
  "cols": 3,
  "rows": 3
}
[/block]