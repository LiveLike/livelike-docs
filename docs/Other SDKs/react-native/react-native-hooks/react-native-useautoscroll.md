---
title: useAutoScroll
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
      slug: useapi
      title: useAPI
---
The `useAutoScroll` hook is responsible for managing auto scroll. For example, when a new message arrive, message list will be auto scrolled to the bottom and the new arrived message will be visible.

##### Example Usage:

```typescript
const listRef = useRef<FlatList>(null);
const { onContentSizeChangeHandler } = useAutoScroll({ ref: listRef });

return (
  <FlatList
    ref={listRef}
    contentContainerStyle={{ flexGrow: 1 }}
    data={messages}
    renderItem={renderListItem}
    keyExtractor={listItemKeyExtractor}
    onContentSizeChange={onContentSizeChangeHandler}
  />
);
```

## Hook Argument

#### `ref`

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
        Ref object of type [Flatlist](https://reactnative.dev/docs/flatlist) component Instance (**Required**)
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

## Hook Return Value

#### `onContentSizeChangeHandler`

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
        Callback function of type: `(width: number, height: number) => void`
      </td>
    </tr>
  </tbody>
</Table>
