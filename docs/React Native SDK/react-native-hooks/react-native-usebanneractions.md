---
title: useBannerActions
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
      slug: react-native-useautohidebannereffect
      title: useAutoHideBannerEffect
---
The purpose of `useBannerActions` hook is to abstract out our store actions and exposes actions handlers responsible for updating store value.  

##### Example usage
[block:code]
{
  "codes": [
    {
      "code": "const { addBannerItem } = useBannerActions();",
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
#### `addBannerItem`
[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-1": "",
    "0-0": "Function of type: \n({ bannerType, bannerMessage }: {bannerType: [BannerType](https://livelike-doc-redirect-url.herokuapp.com/react-native?enum=BannerType); bannerMessage: string;}) => void"
  },
  "cols": 1,
  "rows": 1
}
[/block]