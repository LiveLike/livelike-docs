---
title: LLChatBanner
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
      slug: react-native-llchatmessagemenu
      title: LLChatMessageMenu
---
`LLChatBanner` is rendered in response to any moderation based action for eg Reporting a message, deleting a message or blocking a profile. The banner items are stacked on bottom of each other where each top most item auto hide after a configurable timeout.

<Image width="smart" src="https://files.readme.io/2e23b97-LLChatBanner-doc.png" />

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatBanner,
  LLChatBannerStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      BannerComponent={() => (
        <LLChatBanner bannerTimeout={2000} styles={bannerStyle} />
      )}
    />
  );
}

const bannerStyle: Partial<LLChatBannerStyles> = StyleSheet.create({
  bannerContainer: { top: 10, left: 10 },
});
```

## Hooks used by LLChatBanner

* [useBanner](react-native-usebanner)
* [useAutoHideBannerEffect](react-native-useautohidebannereffect)
* [useStyles](react-native-usestyles)

## LLChatBanner Props

#### `bannerAutoHideTimeout`

Auto hides top most banner item based on given timeout (in ms). 

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
        Number
      </td>

      <td>
        4000 ms
      </td>
    </tr>
  </tbody>
</Table>

#### `BannerItemComponent`

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
        React Component of type [LLChatBannerItem](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItem)
      </td>

      <td>
        [`LLChatBannerItem`](https://docs.livelike.com/docs/react-native-llchatbanner#llchatbanneritem)
      </td>
    </tr>
  </tbody>
</Table>

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatBanner,
  LLChatBannerItemProps,
} from '@livelike/react-native';

function MyBannerItem(props: LLChatBannerItemProps) {
  // render your custom chat header
}

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      BannerComponent={() => (
        <LLChatBanner BannerItemComponent={MyBannerItem} />
      )}
    />
  );
}
```

#### `BannerItemComponentStyles`

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
        [LLChatBannerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItemStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLChatBannerItem` styles.
      </td>
    </tr>
  </tbody>
</Table>

##### Example usage

```typescript
import React from 'react';
import {
  LLChat,
  LLChatBanner,
  LLChatBannerItemStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      BannerComponent={() => (
        <LLChatBanner BannerItemComponentStyles={bannerItemStyle} />
      )}
    />
  );
}

const bannerItemStyle: Partial<LLChatBannerItemStyles> = StyleSheet.create({
  bannerText: { fontSize: 15 },
  itemContainer: { height: 20 },
});
```

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
        StyleSheet of type [LLChatBannerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLChatBanner` styles.
      </td>
    </tr>
  </tbody>
</Table>

#### styles prop details

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
        bannerContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Banner container
      </td>
    </tr>
  </tbody>
</Table>

## LLChatBannerItem

`LLChatBannerItem` component is rendered by the `LLChatBanner` component and represents a single chat banner item

<Image width="80%" src="https://files.readme.io/09e0e3d-Banner-doc-snap.png" />

## Hooks used by LLChatBannerItem

* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLChatBannerItem Props

#### `message`

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

#### `type`

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
        Enum of type [BannerType](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=BannerType)
      </td>

      <td>
        No Default
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
        StyleSheet of type [LLChatBannerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerItemStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLChatBannerItem` styles.
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
        itemContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Banner item container
      </td>
    </tr>

    <tr>
      <td>
        bannerIndicator
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Left indicator in the banner item
      </td>
    </tr>

    <tr>
      <td>
        bannerText
      </td>

      <td>
        [TextStyle](https://reactnative.dev/docs/text-style-props)
      </td>

      <td>
        Text in the banner item
      </td>
    </tr>
  </tbody>
</Table>
