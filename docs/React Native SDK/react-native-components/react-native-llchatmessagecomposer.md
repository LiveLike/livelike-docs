---
title: LLChatMessageComposer
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
      slug: react-native-llchatheader
      title: LLChatHeader
---
LLChatMessageComposer is used to compose a message which could be a text message, image message in the form of stickers of gifs. As part of `LLChat` component this component is rendered at the bottom of the UI.\
LLChatMessageComposer component in turn renders:

* `TextInput` - To send a text message.
* `Sticker Picker` - To pick and send sticker image. Sticker picker component is shown when clicked on sticker picker icon.
* `Gif Picker` - To pick and send gif. Gif picker component is shown when clicked on gif picker icon.

![2152](https://files.readme.io/ea36307-Screenshot_2023-01-27_at_13.26.17.png "Screenshot 2023-01-27 at 13.26.17.png")

##### Custom implementation for `GifPickerComponent`, `StickerPickerComponent` and `SendButtonComponent` example:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageComposer,
  LLChatMessageComposerProps,
  LLGifPickerProps,
  LLStickerPickerProps,
} from '@livelike/react-native';
import { LLComposerSendButtonProps } from '../react-native/src/components/LLChatMessageComposer/LLComposerSendButton';

function MySendButton(props: LLComposerSendButtonProps) {
  // render your custom send button
}

function MyStickerPicker(props: LLStickerPickerProps) {
  // render your custom sticker picker
}

function MyGifPicker(props: LLGifPickerProps) {
  // render your custom gif picker
}

function MyComposer(props: LLChatMessageComposerProps) {
  return (
    <LLChatMessageComposer
      {...props}
      GifPickerComponent={MyGifPicker}
      StickerPickerComponent={MyStickerPicker}
      SendButtonComponent={MySendButton}
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
```

##### Customise styles for Stock `LLGifPicker`, `LLStickerPicker` and `LLComposerSendButton` components example:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageComposer,
  LLChatMessageComposerProps,
  LLComposerSendButtonStyles,
  LLStickerPickerStyles,
  LLGifPickerStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyComposer(props: LLChatMessageComposerProps) {
  return (
    <LLChatMessageComposer
      {...props}
      GifPickerComponentStyles={gifPickerStyles}
      StickerPickerComponentStyles={stickerPickerStyles}
      SendButtonComponentStyles={sendButtonStyles}
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

const sendButtonStyles: Partial<LLComposerSendButtonStyles> = StyleSheet.create(
  {
    buttonContainer: { backgroundColor: 'red' },
    icon: { height: 12, width: 12 },
  }
);
const stickerPickerStyles: Partial<LLStickerPickerStyles> = StyleSheet.create({
  stickerPackIcon: { height: 15, width: 15 },
  stickerImage: { height: 100, width: 100 },
  pickerCloseIcon: { marginLeft: 3 },
});
const gifPickerStyles: Partial<LLGifPickerStyles> = StyleSheet.create({
  gifImage: { height: 100, width: 100 },
  gifImageContainer: { margin: 10 },
});
```

## Hooks used by LLChatMessageComposer

* [useChatMessageActions](react-native-usechatmessageactions)
* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLChatMessageComposer Props

#### `roomId`

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
        String (**Required**)
      </td>

      <td>
        No Default
      </td>
    </tr>
  </tbody>
</Table>

#### `GifPickerComponent`

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
        React Component of type [LLGifPicker](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPicker)
      </td>

      <td>
        [`LLGifPicker`](https://docs.livelike.com/docs/react-native-llgifpicker)
      </td>
    </tr>
  </tbody>
</Table>

#### `GifPickerComponentStyles`

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
        [LLGifPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLGifPickerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLGifPicker` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### `StickerPickerComponent`

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
        React Component of type [LLStickerPicker](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPicker)
      </td>

      <td>
        [`LLStickerPicker`](https://docs.livelike.com/docs/react-native-llstickerpicker)
      </td>
    </tr>
  </tbody>
</Table>

#### `StickerPickerComponentStyles`

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
        [LLStickerPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLStickerPickerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLStickerPicker` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### `SendButtonComponent`

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
        React Component of type [LLComposerSendButton](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButton)
      </td>

      <td>
        [`LLComposerSendButton`](https://docs.livelike.com/docs/react-native-llchatmessagecomposer#llcomposersendbutton)
      </td>
    </tr>
  </tbody>
</Table>

#### `SendButtonComponentStyles`

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
        [LLComposerSendButtonStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButtonStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLComposerSendButton` styles.
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
        StyleSheet of type [LLChatMessageComposerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageComposerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLChatMessageComposer` styles.
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
        composerContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Root composer container
      </td>
    </tr>

    <tr>
      <td>
        composerInput
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        TextInput container
      </td>
    </tr>

    <tr>
      <td>
        composerIcon
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Composer icon for gif and sticker pickers
      </td>
    </tr>
  </tbody>
</Table>

## LLComposerSendButton

`LLComposerSendButton` renders the "Send Message Button" in the `LLChatMessageComposer` component

## Hooks used by LLComposerSendButton

* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLComposerSendButton Props

#### `isSendingMessage`

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
        boolean (**Required**)
      </td>

      <td>
        false
      </td>
    </tr>
  </tbody>
</Table>

#### `disabled`

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

#### `onPress`

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
        StyleSheet of type [LLComposerSendButtonStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLComposerSendButtonStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLComposerSendButton` styles.
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
        buttonContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Send message button container
      </td>
    </tr>

    <tr>
      <td>
        icon
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Button icon styles
      </td>
    </tr>
  </tbody>
</Table>
