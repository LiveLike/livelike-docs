---
title: useApi
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
      slug: usetheme
      title: useTheme
---
The `useAPI` hook is used for invoking API calls and manage the response data accordingly. You should call `onApi` function to fetch and load the data.

##### Example Usage:

```typescript
const fetchData = () => {
  return fetch('<API URL>');
};
const { data, error, isLoading, onApi } = useApi(fetchData);
```

## Hook Argument

#### `apiFunction`

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
        Function of type: () => Promise&lt;unknown&gt; (**Required**)
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `data`

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
        unknown (generic)
      </td>

      <td>
        null
      </td>
    </tr>
  </tbody>
</Table>

#### `error`

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

#### `onApi`

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
        Function of type: () => Promise&lt;unknown&gt;
      </td>
    </tr>
  </tbody>
</Table>