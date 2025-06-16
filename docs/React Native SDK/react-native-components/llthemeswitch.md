---
title: LLThemeSwitch
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
      slug: react-native-customisation
      title: Customisation
---
Using `LLThemeSwitch` component, you can switch between light and dark theme StockUI. The component renders a switch icon to toggle light/dark theme.\
This component is not rendered in Stock UI by default. You can include `LLThemeSwitch` by customising chat header of `LLChat` using [`HeaderComponent`](react-native-llchat#headercomponent) prop

![1794](https://files.readme.io/a13beac-Screenshot_2023-01-30_at_12.04.34.png "Screenshot 2023-01-30 at 12.04.34.png")

##### Example usage:

```typescript
import React from 'react';
import { Text, View } from 'react-native';
import {
  LLChat,
  LLChatHeaderProps,
  LLThemeSwitch,
} from '@livelike/react-native';

function CustomHeader({ title }: LLChatHeaderProps) {
  return (
    <View>
      <Text>{title}</Text>
      <LLThemeSwitch />
    </View>
  );
}

export function MyApp() {
  return <LLChat roomId="<Your chat room id>" HeaderComponent={CustomHeader} />;
}
```

## Hooks used by LLThemeSwitch

* [useTheme](react-native-usetheme)
* [useStyles](react-native-usestyles)

## LLThemeSwitch Props

#### `switchIcon`

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
        [Image source](https://reactnative.dev/docs/image#source)
      </td>

      <td>
        themeAssets.themeSwitch icon (exposed by [useTheme](react-native-usetheme) hook)
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
        StyleSheet of type [LLThemeSwitchStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLThemeSwitchStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal `LLThemeSwitch` styles.
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
        imageContainer
      </td>

      <td>
        [ViewStyle](https://reactnative.dev/docs/view-style-props)
      </td>

      <td>
        Icon image container
      </td>
    </tr>

    <tr>
      <td>
        image
      </td>

      <td>
        [ImageStyle](https://reactnative.dev/docs/image-style-props)
      </td>

      <td>
        Icon image styles
      </td>
    </tr>
  </tbody>
</Table>
