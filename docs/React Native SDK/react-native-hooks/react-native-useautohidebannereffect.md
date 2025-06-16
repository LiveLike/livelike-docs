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

```typescript
const { banners } = useBanner();
useAutoHideBannerEffect({ bannerAutoHideTimeout: 4000 });
```

## Hook Argument

#### `bannerAutoHideTimeout`

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Type
      </th>

      <th>
        Default
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Number (**Required**)
      </td>

      <td>
        4000 (ms)
      </td>
    </tr>
  </tbody>
</Table>
