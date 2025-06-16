---
title: LLChatMessageMenu
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
      slug: react-native-lluserreactioncounts
      title: LLUserReactionCounts
---
## LLChatMessageMenu

`LLChatMessageMenu` is rendered as a popover component. The default user action to show LLChatMessageMenu component is long press on message item. It consists of moderation based menu options like: 

- Report message
- Block profile
- Delete message

![](https://files.readme.io/e670439-Screenshot_2023-01-27_at_10.41.56.png "Screenshot 2023-01-27 at 10.41.56.png")

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItem,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
  LLChatMessageMenu,
  LLChatMessageMenuOption,
  LLChatMessageMenuOptionProps,
  LLChatMessageMenuOptionStyles,
  LLChatMessageMenuProps,
  LLChatMessageMenuStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyMessageMenuOption<OnClickApiFnResponseData extends Promise<any>>(
  props: LLChatMessageMenuOptionProps<OnClickApiFnResponseData>
) {
  return <LLChatMessageMenuOption {...props} styles={messageMenuItemStyle} />;
}

function MyMessageMenu(props: LLChatMessageMenuProps) {
  return <LLChatMessageMenu {...props} styles={messageMenuStyle} />;
}

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  return (
    <LLChatMessageItem
      {...props}
      MessageItemMenuComponent={MyMessageMenu}
      MessageItemMenuOptionComponent={MyMessageMenuOption}
    />
  );
}

function MyMessageListComponent(props: LLChatMessageListProps) {
  return (
    <LLChatMessageList
      {...props}
      MessageItemComponent={MyMessageItemComponent}
    />
  );
}

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}

const messageMenuStyle: Partial<LLChatMessageMenuStyles> = StyleSheet.create({
  menuContainer: { padding: 10 },
});
const messageMenuItemStyle: Partial<LLChatMessageMenuOptionStyles> =
  StyleSheet.create({
    menuItemIcon: { height: 20, width: 20 },
    menuItemText: { fontSize: 12 },
  });
```

### Hooks used by LLChatMessageMenu

- [useStyles](react-native-usestyles)

### LLChatMessageMenu Props

#### `visible`

| Type                   | Default |
| :--------------------- | :------ |
| boolean (**Required**) | false   |

#### \`children'

| Type          | Default                                                                                                            |
| :------------ | :----------------------------------------------------------------------------------------------------------------- |
| React Element | [`LLChatMessageMenuOption`](https://docs.livelike.com/docs/react-native-llchatmessagemenu#llchatmessagemenuoption) |

#### \`styles'

| Type                                                                                                                                       | Default                                                                                             |
| :----------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLChatMessageMenuStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageMenuStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageMenu` styles. |

#### Styles Props

| CSS Class     | Type                                                       | Description         |
| :------------ | :--------------------------------------------------------- | :------------------ |
| menuContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Root menu container |

## LLChatMessageMenuOption

`LLChatMessageMenuOption` represents a single `LLChatMessageMenu` item

### Hooks used by LLChatMessageMenuOption

- [useApi](react-native-useapi)
- [useMessageItemPopover](react-native-usemessageitempopover)
- [useStyles](react-native-usestyles)

### LLChatMessageMenuOption Props

#### `icon`

| Type                                                                     | Default    |
| :----------------------------------------------------------------------- | :--------- |
| [image source](https://reactnative.dev/docs/image#source) (**Required**) | No Default |

#### `textDesc`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `divider`

| Type                                                 | Default      |
| :--------------------------------------------------- | :----------- |
| Object of type: `{ top: boolean; bottom: boolean; }` | Empty Object |

#### `onClickApiFn`

| Type                                             |
| :----------------------------------------------- |
| Function of type: () => OnClickApiFnResponseData |

#### \`styles'

| Type                                                                                                                                                   | Defualt                                                                                                   |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLChatMessageMenuOptionStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageMenuOptionStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageMenuOption` styles. |

#### Styles Props

| CSS Class             | Type                                                         | Description                  |
| :-------------------- | :----------------------------------------------------------- | :--------------------------- |
| menuItem              | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Menu item container          |
| menuItemText          | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Text styles of the menu item |
| menuItemIcon          | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Menu item icon styles        |
| menuItemTopDivider    | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Menu item top divider        |
| menuItemBottomDivider | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Menu item bottom divider     |