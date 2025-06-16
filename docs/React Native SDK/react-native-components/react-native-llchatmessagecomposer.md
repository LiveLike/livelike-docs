---
title: LLChatMessageComposer
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
      slug: react-native-llchatheader
      title: LLChatHeader
---
LLChatMessageComposer is used to compose a message which could be a text message, image message in the form of stickers of gifs. As part of `LLChat` component this component is rendered at the bottom of the UI. 
LLChatMessageComposer component in turn renders:
* `TextInput` - To send a text message.
* `Sticker Picker` - To pick and send sticker image. Sticker picker component is shown when clicked on sticker picker icon.
* `Gif Picker` - To pick and send gif. Gif picker component is shown when clicked on gif picker icon.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ea36307-Screenshot_2023-01-27_at_13.26.17.png",
        "Screenshot 2023-01-27 at 13.26.17.png",
        2152,
        1244,
        "#000000"
      ]
    }
  ]
}
[/block]
##### Custom implementation for `GifPickerComponent`, `StickerPickerComponent` and `SendButtonComponent` example:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatMessageComposer,\n  LLChatMessageComposerProps,\n  LLGifPickerProps,\n  LLStickerPickerProps,\n} from '@livelike/react-native';\nimport { LLComposerSendButtonProps } from '../react-native/src/components/LLChatMessageComposer/LLComposerSendButton';\n\nfunction MySendButton(props: LLComposerSendButtonProps) {\n  // render your custom send button\n}\n\nfunction MyStickerPicker(props: LLStickerPickerProps) {\n  // render your custom sticker picker\n}\n\nfunction MyGifPicker(props: LLGifPickerProps) {\n  // render your custom gif picker\n}\n\nfunction MyComposer(props: LLChatMessageComposerProps) {\n  return (\n    <LLChatMessageComposer\n      {...props}\n      GifPickerComponent={MyGifPicker}\n      StickerPickerComponent={MyStickerPicker}\n      SendButtonComponent={MySendButton}\n    />\n  );\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}",
      "language": "typescript"
    }
  ]
}
[/block]
##### Customise styles for Stock `LLGifPicker`, `LLStickerPicker` and `LLComposerSendButton` components example:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatMessageComposer,\n  LLChatMessageComposerProps,\n  LLComposerSendButtonStyles,\n  LLStickerPickerStyles,\n  LLGifPickerStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nfunction MyComposer(props: LLChatMessageComposerProps) {\n  return (\n    <LLChatMessageComposer\n      {...props}\n      GifPickerComponentStyles={gifPickerStyles}\n      StickerPickerComponentStyles={stickerPickerStyles}\n      SendButtonComponentStyles={sendButtonStyles}\n    />\n  );\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}\n\nconst sendButtonStyles: Partial<LLComposerSendButtonStyles> = StyleSheet.create(\n  {\n    buttonContainer: { backgroundColor: 'red' },\n    icon: { height: 12, width: 12 },\n  }\n);\nconst stickerPickerStyles: Partial<LLStickerPickerStyles> = StyleSheet.create({\n  stickerPackIcon: { height: 15, width: 15 },\n  stickerImage: { height: 100, width: 100 },\n  pickerCloseIcon: { marginLeft: 3 },\n});\nconst gifPickerStyles: Partial<LLGifPickerStyles> = StyleSheet.create({\n  gifImage: { height: 100, width: 100 },\n  gifImageContainer: { margin: 10 },\n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLChatMessageComposer"
}
[/block]
* [useChatMessageActions](react-native-usechatmessageactions)
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLChatMessageComposer Props"
}
[/block]
#### `roomId`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String (**Required**)",
    "0-1": "No Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `GifPickerComponent`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "React Component of type [LLGifPicker](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPicker)",
    "0-1": "[`LLGifPicker`](https://docs.livelike.com/docs/react-native-llgifpicker)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `GifPickerComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLGifPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLGifPicker` styles."
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `StickerPickerComponent`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "React Component of type [LLStickerPicker](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPicker)",
    "0-1": "[`LLStickerPicker`](https://docs.livelike.com/docs/react-native-llstickerpicker)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `StickerPickerComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLStickerPicker` styles.",
    "0-0": "[LLStickerPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPickerStyles)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `SendButtonComponent`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "React Component of type [LLComposerSendButton](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButton)",
    "0-1": "[`LLComposerSendButton`](https://docs.livelike.com/docs/react-native-llchatmessagecomposer#llcomposersendbutton)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `SendButtonComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLComposerSendButton` styles.",
    "0-0": "[LLComposerSendButtonStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButtonStyles)"
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
    "0-1": "No Default, if present styles props would be applied on top of internal `LLChatMessageComposer` styles.",
    "0-0": "StyleSheet of type [LLChatMessageComposerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageComposerStyles)"
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
    "0-0": "composerContainer",
    "1-0": "composerInput",
    "2-0": "composerIcon",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "2-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Root composer container",
    "1-2": "TextInput container",
    "2-2": "Composer icon for gif and sticker pickers"
  },
  "cols": 3,
  "rows": 3
}
[/block]

[block:api-header]
{
  "title": "LLComposerSendButton"
}
[/block]
`LLComposerSendButton` renders the "Send Message Button" in the `LLChatMessageComposer` component
[block:api-header]
{
  "title": "Hooks used by LLComposerSendButton"
}
[/block]
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLComposerSendButton Props"
}
[/block]
#### `isSendingMessage`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "boolean (**Required**)",
    "0-1": "false"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `disabled`
[block:parameters]
{
  "data": {
    "0-0": "boolean",
    "0-1": "false if not present",
    "h-0": "Type",
    "h-1": "Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `onPress`
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
#### `styles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "StyleSheet of type [LLComposerSendButtonStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButtonStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLComposerSendButton` styles."
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
    "0-0": "buttonContainer",
    "1-0": "icon",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Send message button container",
    "1-2": "Button icon styles"
  },
  "cols": 3,
  "rows": 2
}
[/block]