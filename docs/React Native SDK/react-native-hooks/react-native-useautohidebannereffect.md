---
title: useAutoHideBannerEffect
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
      slug: react-native-useautoscroll
      title: useAutoScroll
---
The purpose of `useAutoHideBannerEffect` is to autohide top most displayed banner item after a given time out value (in ms).

##### Example Usage:
[block:code]
{
  "codes": [
    {
      "code": "const { banners } = useBanner();\nuseAutoHideBannerEffect({ bannerAutoHideTimeout: 4000 });",
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
#### `bannerAutoHideTimeout`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "Number (**Required**)",
    "0-1": "4000 (ms)"
  },
  "cols": 2,
  "rows": 1
}
[/block]