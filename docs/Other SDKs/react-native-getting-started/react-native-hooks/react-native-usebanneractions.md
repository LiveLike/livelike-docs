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

```typescript
const { addBannerItem } = useBannerActions();
```

## Hook Return Value

#### `addBannerItem`

<Table align={["left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Function of type:
        (\{ bannerType, bannerMessage }: \{bannerType: [BannerType](https://livelike-doc-redirect-url.herokuapp.com/react-native?enum=BannerType); bannerMessage: string;}) => void
      </td>
    </tr>
  </tbody>
</Table>
