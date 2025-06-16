---
title: useBanner
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
      slug: usebanneractions
      title: useBannerActions
---
The purpose of `useBanner` is to expose the banners state. Internally we are using atomic store for managing the banners state.

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { banners } = useBanner();",
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
#### `banners`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Array of items of type: [Banner](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=Banner)",
    "0-1": "Empty Array"
  },
  "cols": 2,
  "rows": 1
}
[/block]