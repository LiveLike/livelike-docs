---
title: useStickerPacks
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
      slug: useloadstickerpackseffect
      title: useLoadStickerPacksEffect
---
The purpose of `useStickerPacks` hook is to expose sticker packs resource.

##### Example usage

```typescript
const { stickerPacks } = useStickerPacks();
```

## Hook Return Value

#### `stickerPacks`

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
        Array of items of type: [IStickerPack](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IStickerPack)
      </td>

      <td>
        Empty Array
      </td>
    </tr>
  </tbody>
</Table>
