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

```typescript
const { isLoading, gifImages, onGifSearchInputChange, loadNextGifImages } = useGifPicker();
```

## Hook Return Value

#### `gifImages`

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
        Array of [IGif](https://livelike-doc-redirect-url.herokuapp.com/javascript?interface=IGif)
      </td>

      <td>
        Empty Array
      </td>
    </tr>
  </tbody>
</Table>

#### `onGifSearchInputChange`

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
        Function of type: (gifSearchInput, \{ debounce }) => void
      </td>
    </tr>
  </tbody>
</Table>

#### `isLoading`

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
        boolean
      </td>

      <td>
        false
      </td>
    </tr>
  </tbody>
</Table>

#### `loadNextGifImages`

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
