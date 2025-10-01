---
title: useStickerPicker
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
      slug: usegifpicker
      title: useGifPicker
---
The purpose of the `useStickerPicker` is to manage and track the selected sticker pack. It exposes the selected stickerPackId value and appropriate setter function.

##### Example Usage:

```typescript
const { selectedStickerPackId, setSelectedStickerPackId } = useStickerPicker();
```

## Hook Return Value

#### `selectedStickerPackId`

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
        String
      </td>

      <td>
        Empty String
      </td>
    </tr>
  </tbody>
</Table>

#### `setSelectedStickerPackId`

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
        `(newSelectedStickerPickerId) => void`
      </td>
    </tr>
  </tbody>
</Table>
