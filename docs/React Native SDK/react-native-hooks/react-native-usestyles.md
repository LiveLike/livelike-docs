---
title: useStyles
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
The purpose of `useStyles` hook is to merge the default StockUI styles with custom styles provided by the integrator.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "export function LLChatHeader({ title, styles: stylesProp }: LLChatHeaderProps) {\n  const headerStyles = useStyles({\n    componentStylesFn: getChatHeaderStyles,\n    stylesProp,\n  });\n  \n  return (\n    <View style={headerStyles.headerContainer}>\n      <Text style={headerStyles.headerTitle}>{title}</Text>\n    </View>\n  );\n}\n\nconst getChatHeaderStyles: LLComponentStyleFn<LLChatHeaderStyles> = ({\n  theme,\n}) =>\n  StyleSheet.create({\n    headerContainer: {\n      display: 'flex',\n      flexDirection: 'row',\n      padding: 12,\n    },\n    headerTitle: {\n      alignSelf: 'center',\n      fontSize: 16,\n      textAlign: 'center',\n      flex: 1,\n      color: theme.text,\n    },\n  });",
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
#### `componentStylesFn`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: [LLComponentStyleFn](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComponentStyleFn) (**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]
#### `stylesProp`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Partial stylesheet object of type returned by `LLComponentStyleFn`",
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
#### `xxxyyyStyle`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "No Default",
    "0-0": "Stylesheet object of type returned by `LLComponentStyleFn`"
  },
  "cols": 2,
  "rows": 1
}
[/block]