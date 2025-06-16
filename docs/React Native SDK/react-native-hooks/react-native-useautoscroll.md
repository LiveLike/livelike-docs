---
title: useAutoScroll
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
      slug: useapi
      title: useAPI
---
The `useAutoScroll` hook is responsible for managing auto scroll. For example, when a new message arrive, message list will be auto scrolled to the bottom and the new arrived message will be visible.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const listRef = useRef<FlatList>(null);\nconst { onContentSizeChangeHandler } = useAutoScroll({ ref: listRef });\n\nreturn (\n  <FlatList\n    ref={listRef}\n    contentContainerStyle={{ flexGrow: 1 }}\n    data={messages}\n    renderItem={renderListItem}\n    keyExtractor={listItemKeyExtractor}\n    onContentSizeChange={onContentSizeChangeHandler}\n  />\n);",
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
#### `ref`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Ref object of type [Flatlist](https://reactnative.dev/docs/flatlist) component Instance (**Required**)",
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
#### `onContentSizeChangeHandler`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Callback function of type: `(width: number, height: number) => void`"
  },
  "cols": 1,
  "rows": 1
}
[/block]