---
title: useTheme
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
      slug: usestyle
      title: useStyle
---
The purpose of the `useTheme` hook is to manage and customise the StockUI Theme

##### Example Usage:

```typescript
const { theme, themeAssets, setThemeType, setThemes, themeType, themes } = useTheme();
```

## Hook Argument

#### `themeType`

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
        [UseThemeArg](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=UseThemeArg)
      </td>

      <td>
        Empty Object
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `theme`

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
        [LLTheme](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLTheme)
      </td>

      <td>
        Default [colorScheme]()
      </td>
    </tr>
  </tbody>
</Table>

#### `themeAssets`

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
        [LLThemeAssets](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeAssets)
      </td>

      <td>
        Default assets
      </td>
    </tr>
  </tbody>
</Table>

#### `setThemeType`

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
        Function of type: (newThemeType: [LLThemeType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeType)) => void
      </td>
    </tr>
  </tbody>
</Table>

#### `setThemes`

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
        Function of type: (\_themes: [LLThemes](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemes)) => void
      </td>
    </tr>
  </tbody>
</Table>

#### `themeType`

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
        [ColorSchemeName]() | [LLThemeType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=ColorSchemeName)
      </td>

      <td>
        ColorSchemeName
      </td>
    </tr>
  </tbody>
</Table>

#### `themes`

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
        [LLThemes](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemes)
      </td>

      <td>
        Default StockUI Theme
      </td>
    </tr>
  </tbody>
</Table>
