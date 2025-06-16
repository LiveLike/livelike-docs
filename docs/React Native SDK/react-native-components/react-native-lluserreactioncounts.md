---
title: LLUserReactionCounts
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
      slug: react-native-llgifpicker
      title: LLGifPicker
---
## LLUserReactionCounts

`LLUserReactionCounts` is rendered as a message item footer and represents the reaction picker, reactions and reaction count details

![](https://files.readme.io/a546a3f-Screenshot_2023-01-27_at_11.58.25.png "Screenshot 2023-01-27 at 11.58.25.png")

##### Custom implementation for `MessageReactionPickerComponent` and `UserReactionCountDetailComponent` example:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItem,
  LLChatMessageItemFooter,
  LLChatMessageItemFooterProps,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
  LLReactionPickerProps,
  LLUserReactionCountDetailProps,
  LLUserReactionCounts,
  LLUserReactionCountsProps,
} from '@livelike/react-native';

function MyUserReactionsPickerComponent(props: LLReactionPickerProps) {
  // render custom reaction picker component
}

function MyUserReactionsCountDetailComponent(
  props: LLUserReactionCountDetailProps
) {
  // render custom reaction count detail component
}

function MyUserReactionsCountComponent(props: LLUserReactionCountsProps) {
  return (
    <LLUserReactionCounts
      {...props}
      MessageReactionPickerComponent={MyUserReactionsPickerComponent}
      UserReactionCountDetailComponent={MyUserReactionsCountDetailComponent}
    />
  );
}

function MyMessageItemFooter(props: LLChatMessageItemFooterProps) {
  return (
    <LLChatMessageItemFooter
      {...props}
      UserReactionsCountComponent={MyUserReactionsCountComponent}
    />
  );
}

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  return (
    <LLChatMessageItem
      {...props}
      MessageItemFooterComponent={MyMessageItemFooter}
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
```

##### Customise styles for Stock `LLReactionPicker` and `LLUserReactionCountDetail` components example:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItem,
  LLChatMessageItemFooter,
  LLChatMessageItemFooterProps,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
  LLReactionPicker,
  LLReactionPickerItemStyles,
  LLReactionPickerProps,
  LLReactionPickerStyles,
  LLUserReactionCountDetailStyles,
  LLUserReactionCounts,
  LLUserReactionCountsProps,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyUserReactionsPickerComponent(props: LLReactionPickerProps) {
  return (
    <LLReactionPicker
      {...props}
      styles={reactionPickerStyle}
      ReactionItemComponentStyles={reactionItemStyles}
    />
  );
}

function MyUserReactionsCountComponent(props: LLUserReactionCountsProps) {
  return (
    <LLUserReactionCounts
      {...props}
      MessageReactionPickerComponent={MyUserReactionsPickerComponent}
      UserReactionCountDetailComponentStyles={userReactionCountDetailStyles}
    />
  );
}

function MyMessageItemFooter(props: LLChatMessageItemFooterProps) {
  return (
    <LLChatMessageItemFooter
      {...props}
      UserReactionsCountComponent={MyUserReactionsCountComponent}
    />
  );
}

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  return (
    <LLChatMessageItem
      {...props}
      MessageItemFooterComponent={MyMessageItemFooter}
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

const reactionPickerStyle: Partial<LLReactionPickerStyles> = StyleSheet.create({
  pickerContainer: { bottom: 0, right: 0, borderRadius: 10 },
});
const reactionItemStyles: Partial<LLReactionPickerItemStyles> =
  StyleSheet.create({
    reactionIcon: { height: 12, width: 12 },
  });
const userReactionCountDetailStyles: Partial<LLUserReactionCountDetailStyles> =
  StyleSheet.create({
    reactionCountText: { fontSize: 9 },
    reactionIcon: { height: 12, width: 12 },
  });
```

### Hooks used by LLUserReactionCounts

* [useReactionSpace](react-native-reaction-hooks#usereactionspace)
* [useUserReactions](react-native-reaction-hooks#useuserreactions)
* [useStyles](react-native-usestyles)

### LLUserReactionCounts Props

#### `targetGroupId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `targetId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `showReactionPicker`

| Type    | Default              |
| :------ | :------------------- |
| boolean | false if not present |

#### `reactionsLimit`

| Type   | Default |
| :----- | :------ |
| Number | 4       |

#### `onReactionItemPress`

| Type                                                            |
| :-------------------------------------------------------------- |
| Function of type: `(reactionId: string) => void` (**Required**) |

#### `UserReactionCountDetailComponent`

| Type                                                                                                                                                | Default                                                                                                                   |
| :-------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------ |
| React Component of type [LLUserReactionCountDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountDetail) | [`LLUserReactionCountDetail`](https://docs.livelike.com/docs/react-native-lluserreactioncounts#lluserreactioncountdetail) |

#### `UserReactionCountDetailComponentStyles`

| Type                                                                                                                                    | Default                                                                                                     |
| :-------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| [LLUserReactionCountDetailStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountDetailStyles) | No Default, if present styles props would be applied on top of internal `LLUserReactionCountDetail` styles. |

#### `MessageReactionPickerComponent`

| Type                                                                                                                               | Default                                                                                                 |
| :--------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| React Component of type  [LLReactionPicker](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLReactionPicker) | [`LLReactionPicker`](https://docs.livelike.com/docs/react-native-lluserreactioncounts#llreactionpicker) |

#### `MessageReactionPickerComponentStyles`

| Type                                                                                                                                    | Default                                                                                                     |
| :-------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| [LLUserReactionCountDetailStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountDetailStyles) | No Default, if present styles props would be applied on top of internal `LLUserReactionCountDetail` styles. |

#### `styles`

| Type                                                                                                                                             | Default                                                                                                |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLUserReactionCountsStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountsStyles) | No Default, if present styles props would be applied on top of internal `LLUserReactionCounts` styles. |

#### Styles Props

| CSS Class               | Type                                                       | Description                       |
| :---------------------- | :--------------------------------------------------------- | :-------------------------------- |
| reactionCountsContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Reaction counts root container    |
| moreReactionsView       | [ViewStyle](https://reactnative.dev/docs/view-style-props) | More reactions button container   |
| moreReactionsText       | [TextStyle](https://reactnative.dev/docs/text-style-props) | More reactions button text styles |

## LLUserReactionCountDetail

`LLUserReactionCountDetail` represents a single reaction in reaction counts list

### Hooks used by LLUserReactionCountDetail

* [useStyles](react-native-usestyles)

### LLUserReactionCountDetail Props

#### `reaction`

| Type                                                                                                                                     | Default    |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :--------- |
| [IUserReactionCountDetail](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IUserReactionCountDetail) (**Required**) | No Default |

#### `onPress`

| Type                                                            |
| :-------------------------------------------------------------- |
| Function of type: `(reactionId: string) => void` (**Required**) |

#### `styles`

| Type                                                                                                                                                       | Default                                                                                                     |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLUserReactionCountDetailStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountDetailStyles) | No Default, if present styles props would be applied on top of internal `LLUserReactionCountDetail` styles. |

#### Styles Props

| CSS Class             | Type                                                         | Description                     |
| :-------------------- | :----------------------------------------------------------- | :------------------------------ |
| container             | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Root reaction container         |
| reactionIcon          | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Reaction icon styles            |
| reactionCountText     | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Reaction count text styles      |
| selfReactionContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Self reaction root container    |
| selfReactionCountText | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Self reaction count text styles |

## LLReactionPicker

`LLReactionPicker` renders the reaction picker when user press on add reaction icon in message item footer

### Hooks used by LLReactionPicker

* [useReactionPacks](react-native-reaction-hooks#usereactionpacks)
* [useStyles](react-native-usestyles)

### LLReactionPicker Props

#### `visible`

| Type    | Default              |
| :------ | :------------------- |
| boolean | False if not present |

#### `reactionSpaceId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `onPress`

| Type                                                            |
| :-------------------------------------------------------------- |
| Function of type: `(reactionId: string) => void` (**Required**) |

#### `ReactionItemComponent`

| Type                                                                                                                                      | Default                                                                                                         |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| React Component of type [LLReactionPickerItem](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLReactionPickerItem) | [`LLReactionPickerItem`](https://docs.livelike.com/docs/react-native-lluserreactioncounts#llreactionpickeritem) |

#### `ReactionItemComponentStyles`

| Type                                                                                                                          | Default                                                                                                |
| :---------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| [LLReactionPickerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLReactionPickerItemStyles) | No Default, if present styles props would be applied on top of internal `LLReactionPickerItem` styles. |

#### `styles`

| Type                                                                                                                                     | Default                                                                                            |
| :--------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLReactionPickerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLReactionPickerStyles) | No Default, if present styles props would be applied on top of internal `LLReactionPicker` styles. |

#### Styles Props

| CSS Class       | Type                                                       | Description                     |
| :-------------- | :--------------------------------------------------------- | :------------------------------ |
| pickerContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Root reactions picker container |

## LLReactionPickerItem

`LLReactionPickerItem` renders a single reaction in reaction picker

### Hooks used by LLReactionPickerItem

* [useStyles](react-native-usestyles)

### LLReactionPickerItem Props

#### `reaction`

| Type                                                                                                                 | Default    |
| :------------------------------------------------------------------------------------------------------------------- | :--------- |
| [IReactionEmoji](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IReactionEmoji) (**Required**) | No Default |

#### `onPress`

| Type                                                    |
| :------------------------------------------------------ |
| Function of type: `(id: string) => void` (**Required**) |

#### `styles`

| Type                                                                                                                                             | Default                                                                                                |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLReactionPickerItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLReactionPickerItemStyles) | No Default, if present styles props would be applied on top of internal `LLReactionPickerItem` styles. |

#### Styles Props

| CSS Class    | Type                                                         | Description                               |
| :----------- | :----------------------------------------------------------- | :---------------------------------------- |
| reactionIcon | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Reaction icon styles (in reaction picker) |
