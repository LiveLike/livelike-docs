---
title: LLStickerPicker
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
      slug: llthemeswitch
      title: LLThemeSwitch
---
`LLGifPicker` renders a Sticker picker component when a user press on sticker-picker icon in composer

![1810](https://files.readme.io/2e75341-Screenshot_2023-01-30_at_11.04.10.png "Screenshot 2023-01-30 at 11.04.10.png")

##### Customise styles for Stock `LLStickerPicker` component example:

```typescript
import React from 'react';
import {
  LLBasePickerStyles,
  LLChat,
  LLChatMessageComposer,
  LLChatMessageComposerProps,
  LLStickerPicker,
  LLStickerPickerProps,
  LLStickerPickerStyles,
  useTheme,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';
import { useMemo } from 'react';

function MyStickerPicker(props: LLStickerPickerProps) {
  const { themeType } = useTheme();
  const pickerComponentStyles = useMemo(() => pickerComponentStylesFn(themeType), [themeType]);

  return (
    <LLStickerPicker
      {...props}
      PickerComponentStyles={pickerComponentStyles}
      styles={gifPickerStyles}
    />
  );
}

function MyComposer(props: LLChatMessageComposerProps) {
  return (
    <LLChatMessageComposer
      {...props}
      StickerPickerComponent={MyStickerPicker}
    />
  );
}

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageComposerComponent={MyComposer}
    />
  );
}

const gifPickerStyles: Partial<LLStickerPickerStyles> = StyleSheet.create({
  pickerCloseIcon: { height: 12, width: 12 },
  stickerImage: { width: 70, height: 70 },
  stickerPackIcon: { height: 22, width: 22 },
});
const pickerComponentStylesFn: (
  theme: 'light' | 'dark'
) => Partial<LLBasePickerStyles> = (theme) =>
  StyleSheet.create({
    pickerContainer: {
      minHeight: 250,
      maxHeight: 350,
      backgroundColor: theme === 'light' ? '#A0C3D2' : '#2b4956',
    },
    pickerItemsScrollview: {
      padding: 10,
    },
  });
```

## Hooks used by LLStickerPicker

* [useStickerPacks](react-native-usestickerpacks)
* [useStickerPicker](react-native-usestickerpicker)
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLStickerPicker Props

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

#### `closeStickerPicker`

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

#### `onSelectSticker`

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
        Function of type: `(stickerShortcode: string) => void` (**Required**)
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

      </th>

      <th>

      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        StyleSheet of type [LLStickerPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPickerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLStickerPicker` styles.
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
        stickerPacksContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Sticker packs item container
      </td>
    </tr>

    <tr>
      <td>
        stickerImageContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Sticker item container
      </td>
    </tr>

    <tr>
      <td>
        stickerHeaderContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Root sticker packs container
      </td>
    </tr>

    <tr>
      <td>
        stickerPackIcon
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Sticker packs item styles
      </td>
    </tr>

    <tr>
      <td>
        stickerImage
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Sticker item styles
      </td>
    </tr>

    <tr>
      <td>
        pickerCloseIcon
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Sticker picker close icon styles
      </td>
    </tr>
  </tbody>
</Table>
