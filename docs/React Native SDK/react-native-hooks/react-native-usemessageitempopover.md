---
title: useMessageItemPopover
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
      slug: react-native-usestickerpack
      title: useStickerPack
---
The purpose of `useMessageItemPopover` is to control the presence of the popover menu, using exposed states and functions.

##### Example Usage:

```typescript
const { popoverDetail, showPopover, hidePopover } = useMessageItemPopover({
  messageId: <Message ID>,
});
```

## Hook Argument

#### `messageId`

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
        No Default
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `popoverDetail`

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
        [PopoverDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=PopoverDetail)
      </td>

      <td>
        \{ messageId: '', popoverType: undefined }
      </td>
    </tr>
  </tbody>
</Table>

#### `showPopover`

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
        Function of type: (args: [PopoverDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=PopoverDetail)) => void
      </td>
    </tr>
  </tbody>
</Table>

#### `hidePopover`

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
        Function of type: `() => void`
      </td>
    </tr>
  </tbody>
</Table>
