---
title: LLThemeSwitch
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
      slug: react-native-customisation
      title: Customisation
---
Using `LLThemeSwitch` component, you can switch between light and dark theme StockUI. The component renders a switch icon to toggle light/dark theme.
This component is not rendered in Stock UI by default. You can include `LLThemeSwitch` by customising chat header of `LLChat` using [`HeaderComponent`](react-native-llchat#headercomponent) prop
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a13beac-Screenshot_2023-01-30_at_12.04.34.png",
        "Screenshot 2023-01-30 at 12.04.34.png",
        1794,
        1536,
        "#000000"
      ]
    }
  ]
}
[/block]
##### Example usage:
[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport { Text, View } from 'react-native';\nimport {\n  LLChat,\n  LLChatHeaderProps,\n  LLThemeSwitch,\n} from '@livelike/react-native';\n\nfunction CustomHeader({ title }: LLChatHeaderProps) {\n  return (\n    <View>\n      <Text>{title}</Text>\n      <LLThemeSwitch />\n    </View>\n  );\n}\n\nexport function MyApp() {\n  return <LLChat roomId=\"<Your chat room id>\" HeaderComponent={CustomHeader} />;\n}",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hooks used by LLThemeSwitch"
}
[/block]
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)
[block:api-header]
{
  "title": "LLThemeSwitch Props"
}
[/block]
#### `switchIcon`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[Image source](https://reactnative.dev/docs/image#source)",
    "0-1": "themeAssets.themeSwitch icon (exposed by [useTheme](react-native-usetheme) hook)"
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
    "0-0": "StyleSheet of type [LLThemeSwitchStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeSwitchStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLThemeSwitch` styles."
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
    "0-0": "imageContainer",
    "1-0": "image",
    "0-1": "[ViewStyle](https://reactnative.dev/docs/view-style-props)",
    "1-1": "[ImageStyle](https://reactnative.dev/docs/image-style-props)",
    "0-2": "Icon image container",
    "1-2": "Icon image styles"
  },
  "cols": 3,
  "rows": 2
}
[/block]