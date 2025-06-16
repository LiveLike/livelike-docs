---
title: LLChatBanner
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
      slug: react-native-llchatmessagemenu
      title: LLChatMessageMenu
---
`LLChatBanner` is rendered in response to any moderation based action for eg Reporting a message, deleting a message or blocking a profile. The banner items are stacked on bottom of each other where each top most item auto hide after a configurable timeout.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2e23b97-LLChatBanner-doc.png",
        "LLChatBanner-doc.png",
        2730,
        2121,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]
##### Example usage:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatBanner,\n  LLChatBannerStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      BannerComponent={() => (\n        <LLChatBanner bannerTimeout={2000} styles={bannerStyle} />\n      )}\n    />\n  );\n}\n\nconst bannerStyle: Partial<LLChatBannerStyles> = StyleSheet.create({\n  bannerContainer: { top: 10, left: 10 },\n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLChatBanner"
}
[/block]
* [useBanner](react-native-usebanner)
* [useAutoHideBannerEffect](react-native-useautohidebannereffect)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLChatBanner Props"
}
[/block]
#### `bannerAutoHideTimeout`
Auto hides top most banner item based on given timeout (in ms). 
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Number",
    "0-1": "4000 ms"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `BannerItemComponent`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "React Component of type [LLChatBannerItem](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItem)",
    "0-1": "[`LLChatBannerItem`](https://docs.livelike.com/docs/react-native-llchatbanner#llchatbanneritem)"
  },
  "cols": 2,
  "rows": 1
}
[/block]
##### Example usage:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatBanner,\n  LLChatBannerItemProps,\n} from '@livelike/react-native';\n\nfunction MyBannerItem(props: LLChatBannerItemProps) {\n  // render your custom chat header\n}\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      BannerComponent={() => (\n        <LLChatBanner BannerItemComponent={MyBannerItem} />\n      )}\n    />\n  );\n}",
      "language": "typescript"
    }
  ]
}
[/block]
#### `BannerItemComponentStyles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLChatBannerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItemStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLChatBannerItem` styles."
  },
  "cols": 2,
  "rows": 1
}
[/block]
##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatBanner,\n  LLChatBannerItemStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      BannerComponent={() => (\n        <LLChatBanner BannerItemComponentStyles={bannerItemStyle} />\n      )}\n    />\n  );\n}\n\nconst bannerItemStyle: Partial<LLChatBannerItemStyles> = StyleSheet.create({\n  bannerText: { fontSize: 15 },\n  itemContainer: { height: 20 },\n});",
      "language": "typescript"
    }
  ]
}
[/block]
#### `styles`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "StyleSheet of type [LLChatBannerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLChatBanner` styles."
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### styles prop details
[block:parameters]
{
  "data": {
    "h-0": "CSS Class",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "bannerContainer",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "0-2": "Banner container"
  },
  "cols": 3,
  "rows": 1
}
[/block]

[block:api-header]
{
  "title": "LLChatBannerItem"
}
[/block]
`LLChatBannerItem` component is rendered by the `LLChatBanner` component and represents a single chat banner item
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/09e0e3d-Banner-doc-snap.png",
        "Banner-doc-snap.png",
        1632,
        1086,
        "#000000"
      ],
      "sizing": "80"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLChatBannerItem"
}
[/block]
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLChatBannerItem Props"
}
[/block]
#### `message`
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
#### `type`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Enum of type [BannerType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=BannerType)",
    "0-1": "No Default"
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
    "0-0": "StyleSheet of type [LLChatBannerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItemStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLChatBannerItem` styles."
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
    "0-0": "itemContainer",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "0-2": "Banner item container",
    "1-0": "bannerIndicator",
    "1-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "2-0": "bannerText",
    "2-1": "[TextStyle](https://reactnative.dev/docs/text-style-props)",
    "1-2": "Left indicator in the banner item",
    "2-2": "Text in the banner item"
  },
  "cols": 3,
  "rows": 3
}
[/block]