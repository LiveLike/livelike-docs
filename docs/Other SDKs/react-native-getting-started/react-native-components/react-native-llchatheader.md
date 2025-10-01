---
title: LLChatHeader
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
      slug: react-native-llchatbanner
      title: LLChatBanner
---
`LLChatHeader` represents the ChatUI Header and it is rendered at the top of the Chat UI

![1700](https://files.readme.io/209755b-Screenshot_2023-01-25_at_14.18.18.png "Screenshot 2023-01-25 at 14.18.18.png")

##### Standalone example usage:

```typescript
import React from 'react';
import { StyleSheet, View } from 'react-native';
import { LLChatHeader, LLChatHeaderStyles } from '@livelike/react-native';
import { Body, Footer } from '../components';

export function MyApp() {
  return (
    <View>
      <LLChatHeader title="My Header" styles={headerStyle} />
      <Body />
      <Footer />
    </View>
  );
}

const headerStyle: Partial<LLChatHeaderStyles> = StyleSheet.create({
  headerContainer: { padding: 10 },
  headerTitle: { fontSize: 15 },
});
```

##### Usage for customising `ChatHeader` for ChatUI:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatHeader,
  LLChatHeaderStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      HeaderComponent={() => (
        <LLChatHeader title="My Chatroom" styles={headerStyle} />
      )}
    />
  );
}

const headerStyle: Partial<LLChatHeaderStyles> = StyleSheet.create({
  headerContainer: { padding: 10 },
  headerTitle: { fontSize: 15 },
});
```

## Hooks used by LLChatHeader

* [useStyles](react-native-usestyles)

## LLChatHeader Props

#### `title`

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
        StyleSheet of type [LLChatHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatHeaderStyles)
      </td>

      <td>
        No Default, if present styles props would be applied on top of internal styles of type [LLChatHeaderStyles](react-native-llchatheader#styles)
      </td>
    </tr>
  </tbody>
</Table>

### styles Props

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
        Header container
      </td>
    </tr>

    <tr>
      <td>
        headerTitle
      </td>

      <td>
        [TextStyle](https://reactnative.dev/docs/text-style-props)
      </td>

      <td>
        Text in the header container
      </td>
    </tr>
  </tbody>
</Table>
