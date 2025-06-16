---
title: LLGifPicker
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
      slug: react-native-llstickerpicker
      title: LLStickerPicker
---
`LLGifPicker` renders a Gif picker component when a user press on gif-picker icon in composer\
The component consists of:

* `Header` - Search input and close button
* `Picker` - Gifs based on search result

![1916](https://files.readme.io/fb7da9f-Screenshot_2023-01-28_at_16.24.34.png "Screenshot 2023-01-28 at 16.24.34.png")

> 🚧 GIFs are not supported by default on Android
>
> You will need to add **com.facebook.fresco:animated-gif:2.+** as an additional dependency to **android/app/build.gradle**\
> [Read more...](https://reactnative.dev/docs/0.62/image#gif-and-webp-support-on-android)

##### Custom implementation for `GifPickerHeaderComponent` example:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageComposer,
  LLChatMessageComposerProps,
  LLGifPicker,
  LLGifPickerHeaderProps,
  LLGifPickerProps,
  LLGifPickerStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyGifPickerHeader(props: LLGifPickerHeaderProps) {
  // Render your custom gif picker header
}

function MyGifPicker(props: LLGifPickerProps) {
  return (
    <LLGifPicker
      {...props}
      GifPickerHeaderComponent={MyGifPickerHeader}
    />
  );
}

function MyComposer(props: LLChatMessageComposerProps) {
  return <LLChatMessageComposer {...props} GifPickerComponent={MyGifPicker} />;
}

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageComposerComponent={MyComposer}
    />
  );
}
```

##### Customise styles for Stock `LLGifPicker`, `LLGifPickerHeader` and `LLBasePicker` component example:

```typescript
import React from 'react';
import {
  LLBasePickerStyles,
  LLChat,
  LLChatMessageComposer,
  LLChatMessageComposerProps,
  LLGifPicker,
  LLGifPickerHeaderStyles,
  LLGifPickerProps,
  LLGifPickerStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyGifPicker(props: LLGifPickerProps) {
  return (
    <LLGifPicker
      {...props}
      GifPickerHeaderComponentStyles={gifPickerHeaderStyles}
      PickerComponentStyles={gifPickerComponentStyles}
      styles={gifPickerStyles}
    />
  );
}

function MyComposer(props: LLChatMessageComposerProps) {
  return <LLChatMessageComposer {...props} GifPickerComponent={MyGifPicker} />;
}

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageComposerComponent={MyComposer}
    />
  );
}

const gifPickerStyles: Partial<LLGifPickerStyles> = StyleSheet.create({
  gifImage: { height: 100, width: 100 },
  gifImageContainer: { margin: 10 },
});
const gifPickerHeaderStyles: Partial<LLGifPickerHeaderStyles> =
  StyleSheet.create({
    headerContainer: { padding: 5 },
    searchInput: { borderRadius: 10, height: 50, padding: 10 },
    closeIcon: { height: 30, width: 30 },
  });
const gifPickerComponentStyles: Partial<LLBasePickerStyles> = StyleSheet.create(
  {
    pickerContainer: {
      minHeight: 250,
      maxHeight: 350,
      backgroundColor: 'white',
    },
    pickerItemsScrollview: {
      padding: 10,
    },
  }
);
```

## Hooks used by LLGifPicker

* [useGifPicker](react-native-usegifpicker)
* [useStyles](react-native-usestyles)

## LLGifPicker Props

#### `visible`

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
        false if not present
      </td>
    </tr>
  </tbody>
</Table>

#### `closeGifPicker`

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

#### `onSelectGif`

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
        Function of type: (gifImage: [IGif](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IGif)) => void (**Required**)
      </td>
    </tr>
  </tbody>
</Table>

#### `GifPickerHeaderComponent`

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
        React Component of type [LLGifPickerHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeader)
      </td>

      <td>
        [`LLGifPickerHeader`](https://docs.livelike.com/docs/react-native-llgifpicker#llgifpickerheader)
      </td>
    </tr>
  </tbody>
</Table>

#### `GifPickerHeaderComponentStyles`

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
        [LLGifPickerHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeaderStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLGifPickerHeader` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### `PickerComponentStyles`

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
        [LLBasePickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLBasePickerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLBasePicker` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### `styles`

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
        StyleSheet of type [LLGifPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLGifPicker` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### Styles Props

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        CSS Class
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        gifImageContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Gif image container styles
      </td>
    </tr>

    <tr>
      <td>
        gifImage
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Gif image styles
      </td>
    </tr>
  </tbody>
</Table>

## LLGifPickerHeader

`LLGifPickerHeader` renders a header of the gif picker component and consists of search input and close button

## Hooks used by LLGifPickerHeader

* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLGifPickerHeader Props

#### `onSearchInputChange`

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
        Function of type:
        `(gifSearchInput: string, options?: { debounce: boolean;}) => void`
        (**Required**)
      </td>
    </tr>
  </tbody>
</Table>

#### `closeGifPicker`

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
        (**Required**)
      </td>
    </tr>
  </tbody>
</Table>

#### `styles`

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
        StyleSheet of type [LLGifPickerHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerHeaderStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLGifPickerHeader` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### Style Props

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        CSS Class
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        headerContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Root header container
      </td>
    </tr>

    <tr>
      <td>
        searchInput
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Search input styles
      </td>
    </tr>

    <tr>
      <td>
        closeIcon
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Close icon styles
      </td>
    </tr>
  </tbody>
</Table>
