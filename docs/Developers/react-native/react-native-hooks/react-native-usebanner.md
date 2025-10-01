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

```typescript
const { banners } = useBanner();
```

## Hook Return Value

#### `banners`

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
        Array of items of type: [Banner](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=Banner)
      </td>

      <td>
        Empty Array
      </td>
    </tr>
  </tbody>
</Table>
