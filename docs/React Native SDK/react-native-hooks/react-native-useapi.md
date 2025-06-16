---
title: useApi
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
      slug: usetheme
      title: useTheme
---
The `useAPI` hook is used for invoking API calls and manage the response data accordingly. You should call `onApi` function to fetch and load the data.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const fetchData = () => {\n  return fetch('<API URL>');\n};\nconst { data, error, isLoading, onApi } = useApi(fetchData);",
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
#### `apiFunction`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: () => Promise<unknown> (**Required**)"
  },
  "cols": 1,
  "rows": 1
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `data`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "unknown (generic)",
    "0-1": "null"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `error`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "String",
    "0-1": "Empty String"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `isLoading`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "boolean",
    "0-1": "false"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `onApi`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "0-0": "Function of type: () => Promise<unknown>"
  },
  "cols": 1,
  "rows": 1
}
[/block]