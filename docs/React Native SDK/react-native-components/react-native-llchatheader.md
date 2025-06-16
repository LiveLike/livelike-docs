---
title: LLChatHeader
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
      slug: react-native-llchatbanner
      title: LLChatBanner
---
`LLChatHeader` represents the ChatUI Header and it is rendered at the top of the Chat UI
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/209755b-Screenshot_2023-01-25_at_14.18.18.png",
        "Screenshot 2023-01-25 at 14.18.18.png",
        1700,
        1614,
        "#000000"
      ]
    }
  ]
}
[/block]
##### Standalone example usage:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport { StyleSheet, View } from 'react-native';\nimport { LLChatHeader, LLChatHeaderStyles } from '@livelike/react-native';\nimport { Body, Footer } from '../components';\n\nexport function MyApp() {\n  return (\n    <View>\n      <LLChatHeader title=\"My Header\" styles={headerStyle} />\n      <Body />\n      <Footer />\n    </View>\n  );\n}\n\nconst headerStyle: Partial<LLChatHeaderStyles> = StyleSheet.create({\n  headerContainer: { padding: 10 },\n  headerTitle: { fontSize: 15 },\n});",
      "language": "typescript"
    }
  ]
}
[/block]
##### Usage for customising `ChatHeader` for ChatUI:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport {\n  LLChat,\n  LLChatHeader,\n  LLChatHeaderStyles,\n} from '@livelike/react-native';\nimport { StyleSheet } from 'react-native';\n\nexport function MyApp() {\n  return (\n    <LLChat\n      roomId=\"<Your chat room id>\"\n      HeaderComponent={() => (\n        <LLChatHeader title=\"My Chatroom\" styles={headerStyle} />\n      )}\n    />\n  );\n}\n\nconst headerStyle: Partial<LLChatHeaderStyles> = StyleSheet.create({\n  headerContainer: { padding: 10 },\n  headerTitle: { fontSize: 15 },\n});",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLChatHeader"
}
[/block]
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLChatHeader Props"
}
[/block]
#### `title`
[block:parameters]
{
  "data": {
    "0-0": "String (**Required**)",
    "h-0": "Type",
    "h-1": "Default",
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
    "0-0": "StyleSheet of type [LLChatHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatHeaderStyles)",
    "h-0": "Type",
    "0-1": "No Default, if present styles props would be applied on top of internal styles of type [LLChatHeaderStyles](react-native-llchatheader#styles)",
    "h-1": "Default"
  },
  "cols": 2,
  "rows": 1
}
[/block]
### styles Props
[block:parameters]
{
  "data": {
    "h-0": "CSS Class",
    "h-1": "Type",
    "h-2": "Description",
    "0-0": "headerContainer",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "0-2": "Header container",
    "1-0": "headerTitle",
    "1-1": "[TextStyle](https://reactnative.dev/docs/text-style-props)",
    "1-2": "Text in the header container"
  },
  "cols": 3,
  "rows": 2
}
[/block]