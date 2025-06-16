---
title: useStyles
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
The purpose of `useStyles` hook is to merge the default StockUI styles with custom styles provided by the integrator.

##### Example Usage:

```typescript
export function LLChatHeader({ title, styles: stylesProp }: LLChatHeaderProps) {
  const headerStyles = useStyles({
    componentStylesFn: getChatHeaderStyles,
    stylesProp,
  });
  
  return (
    <View style={headerStyles.headerContainer}>
      <Text style={headerStyles.headerTitle}>{title}</Text>
    </View>
  );
}

const getChatHeaderStyles: LLComponentStyleFn<LLChatHeaderStyles> = ({
  theme,
}) =>
  StyleSheet.create({
    headerContainer: {
      display: 'flex',
      flexDirection: 'row',
      padding: 12,
    },
    headerTitle: {
      alignSelf: 'center',
      fontSize: 16,
      textAlign: 'center',
      flex: 1,
      color: theme.text,
    },
  });
```

## Hook Argument

#### `componentStylesFn`

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
        Function of type: [LLComponentStyleFn](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComponentStyleFn) (**Required**)
      </td>
    </tr>
  </tbody>
</Table>

#### `stylesProp`

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
        Partial stylesheet object of type returned by `LLComponentStyleFn`
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `xxxyyyStyle`

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
        Stylesheet object of type returned by `LLComponentStyleFn`
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>
