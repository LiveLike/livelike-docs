---
title: useTheme
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
      slug: usestyle
      title: useStyle
---
The purpose of the `useTheme` hook is to manage and customise the StockUI Theme

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { theme, themeAssets, setThemeType, setThemes, themeType, themes } = useTheme();",
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
#### `themeType`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[UseThemeArg](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=UseThemeArg)",
    "0-1": "Empty Object"
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
#### `theme`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLTheme](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTheme)",
    "0-1": "Default [colorScheme]()"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `themeAssets`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLThemeAssets](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeAssets)",
    "0-1": "Default assets"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `setThemeType`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: (newThemeType: [LLThemeType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeType)) => void"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `setThemes`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: (_themes: [LLThemes](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemes)) => void"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `themeType`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[ColorSchemeName]() | [LLThemeType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=ColorSchemeName)",
    "0-1": "ColorSchemeName"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `themes`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "[LLThemes](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemes)",
    "0-1": "Default StockUI Theme"
  },
  "cols": 2,
  "rows": 1
}
[/block]