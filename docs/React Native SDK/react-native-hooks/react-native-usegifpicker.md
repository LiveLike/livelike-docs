---
title: useGifPicker
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
The purpose of `useGifPicker` hook is to manage and expose the gif picker resources.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { isLoading, gifImages, onGifSearchInputChange, loadNextGifImages } = useGifPicker();",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Hook Return Value"
}
[/block]
#### `gifImages`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Array of [IGif](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IGif)",
    "0-1": "Empty Array"
  },
  "cols": 2,
  "rows": 1
}
[/block]
#### `onGifSearchInputChange`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Function of type: (gifSearchInput, { debounce }) => void"
  },
  "cols": 1,
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
#### `loadNextGifImages`
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