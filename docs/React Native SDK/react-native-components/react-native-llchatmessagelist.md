---
title: LLChatMessageList
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
## LLChatMessageList

`LLChatMessageList` component represents the chat message list. Internally we render `FlatList` component from `react-native`.

![](https://files.readme.io/c25e488-Screenshot_2023-01-26_at_11.59.35.png "Screenshot 2023-01-26 at 11.59.35.png")

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageList,
  LLChatMessageListStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={(props) => (
        <LLChatMessageList {...props} styles={messageListStyle} />
      )}
    />
  );
}

const messageListStyle: Partial<LLChatMessageListStyles> = StyleSheet.create({
  rootContainer: { padding: 10 },
});
```

### Hooks used by LLChatMessageList

- [useAutoScroll](react-native-useautoscroll)
- [useStyles](react-native-usestyles)
- [useTheme](react-native-usetheme)
- [useReactionSpace](react-native-reaction-hooks#usereactionspace)
- [useChatMessagesEffect](react-native-usechatmessageseffect)
- [useLoadReactionPacksEffect](react-native-reaction-hooks#useloadreactionpackseffect)
- [useUserReactionEffect](react-native-reaction-hooks#useuserreactioneffect)
- [useChatMessages](react-native-usechatmessages)
- [useLoadUserReactions](react-native-reaction-hooks#useloaduserreactions)

### LLChatMessageList Props

#### `roomId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

#### `MessageItemComponent`

| Type                                                                                                                                | Default                                                                 |
| :---------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------- |
| React Component of type [LLChatMessageItem](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItem) | [`LLChatMessageItem`](react-native-llchatmessagelist#llchatmessageitem) |

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
} from '@livelike/react-native';

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  // render your custom chat header
}

const MyMessageListComponent = (props: LLChatMessageListProps) => {
  return (
    <LLChatMessageList
      {...props}
      MessageItemComponent={MyMessageItemComponent}
    />
  );
};

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}
```

#### `MessageItemComponentStyles`

| Type                                                                                                                    | Default                                                                                           |
| :---------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| [LLChatMessageItemStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemStyles) | No Default, if present styles props would be applied on top of internal LLChatMessageItem styles. |

##### Example usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItemStyles,
  LLChatMessageList,
  LLChatMessageListProps,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

const MyMessageListComponent = (props: LLChatMessageListProps) => {
  return (
    <LLChatMessageList
      {...props}
      MessageItemComponentStyles={messageItemStyles}
    />
  );
};

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}

const messageItemStyles: Partial<LLChatMessageItemStyles> = StyleSheet.create({
  messageItemContainer: { backgroundColor: 'darkgrey', marginVertical: 20 },
  selfMessageItemContainer: { backgroundColor: 'red' },
});
```

#### `MessageListEmptyComponent`

| Type                                                                                                                                                    | Default                                                                                   |
| :------------------------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------- |
| React Component of type [LLMessageListEmptyComponent](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLMessageListEmptyComponent) | [`LLMessageListEmptyComponent`](react-native-llchatmessagelist#messagelistemptycomponent) |

##### Example Usage:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageList,
  LLChatMessageListProps,
  LLMessageListEmptyComponentProps,
} from '@livelike/react-native';

function MyMessageListEmptyComponent(props: LLMessageListEmptyComponentProps) {
  // render your custom message list empty component 
}

const MyMessageListComponent = (props: LLChatMessageListProps) => {
  return (
    <LLChatMessageList
      {...props}
      MessageListEmptyComponent={MyMessageListEmptyComponent}
    />
  );
};

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}
```

#### `MessageListEmptyComponentStyles`

| Type                                                                                                                                        | Default                                                                                                     |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------------------------------------------------------- |
| [LLMessageListEmptyComponentStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLMessageListEmptyComponentStyles) | No Default, if present styles props would be applied on top of internal LLMessageListEmptyComponent styles. |

#### `styles`

| Type                                                                                                                                       | Default                                                                                           |
| :----------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------ |
| StyleSheet of type [LLChatMessageListStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageListStyles) | No Default, if present styles props would be applied on top of internal LLChatMessageList styles. |

#### Styles Props

| CSS Class            | Type                                                       | Description              |
| :------------------- | :--------------------------------------------------------- | :----------------------- |
| rootContainer        | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Message list container   |
| listLoadingIndicator | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Loading indicator styles |

## LLChatMessageItem

`LLChatMessageItem` represents a single message in message list and consists of header, body and footer.

![](https://files.readme.io/2ac1ebd-Screenshot_2023-01-26_at_16.24.06.png "Screenshot 2023-01-26 at 16.24.06.png")

### Hooks used by LLChatMessageItem

- [useMessageItemPopover](react-native-usemessageitempopover)
- [useTheme](react-native-usetheme)
- [useStyles](react-native-usestyles)

### LLChatMessageItem Props

#### `message`

| Type                                                                                                             | Default    |
| :--------------------------------------------------------------------------------------------------------------- | :--------- |
| [IChatMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatMessage) (**Required**) | No Default |

#### `MessageItemHeaderComponent`

| Type                                                                                                                                            | Default                                                                                                            |
| :---------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| React Component of type [LLChatMessageItemHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemHeader) | [`LLChatMessageItemHeader`](https://docs.livelike.com/docs/react-native-llchatmessagelist#llchatmessageitemheader) |

#### `MessageItemBodyComponent`

| Type                                                                                                                                        | Default                                                                                                        |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------- |
| React Component of type [LLChatMessageItemBody](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBody) | [`LLChatMessageItemBody`](https://docs.livelike.com/docs/react-native-llchatmessagelist#llchatmessageitembody) |

#### `MessageItemFooterComponent`

| Type                                                                                                                                            | Default                                                                                                            |
| :---------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| React Component of type [LLChatMessageItemFooter](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemFooter) | [`LLChatMessageItemFooter`](https://docs.livelike.com/docs/react-native-llchatmessagelist#llchatmessageitemfooter) |

##### Example usage for `MessageItemHeaderComponent`, `MessageItemBodyComponent` and `MessageItemFooterComponent` props:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItem,
  LLChatMessageItemBodyProps,
  LLChatMessageItemFooterProps,
  LLChatMessageItemHeaderProps,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
} from '@livelike/react-native';

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  return (
    <LLChatMessageItem
      {...props}
      MessageItemHeaderComponent={(props: LLChatMessageItemHeaderProps) => {
        // render your custom message item header
      }}
      MessageItemBodyComponent={(props: LLChatMessageItemBodyProps) => {
        // render your custom message item body
      }}
      MessageItemFooterComponent={(props: LLChatMessageItemFooterProps) => {
        // render your custom message item footer
      }}
    />
  );
}

const MyMessageListComponent = (props: LLChatMessageListProps) => {
  return (
    <LLChatMessageList
      {...props}
      MessageItemComponent={MyMessageItemComponent}
    />
  );
};

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}
```

#### `MessageItemHeaderComponentStyles`

| Type                                                                                                                                | Default                                                                                                   |
| :---------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| [LLChatMessageItemHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemHeaderStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemHeader` styles. |

#### `MessageItemBodyComponentStyles`

| Type                                                                                                                            | Default                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------ |
| [LLChatMessageItemBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBodyStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemBody` styles. |

#### `MessageItemFooterComponentStyles`

| Type                                                                                                                                | Default                                                                                                   |
| :---------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| [LLChatMessageItemFooterStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemFooterStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemFooter` styles. |

##### Example usage for `MessageItemHeaderComponentStyles`, `MessageItemBodyComponentStyles` and `MessageItemFooterComponentStyles` props:

```typescript
import React from 'react';
import {
  LLChat,
  LLChatMessageItem,
  LLChatMessageItemBodyStyles,
  LLChatMessageItemFooterStyles,
  LLChatMessageItemHeaderStyles,
  LLChatMessageItemProps,
  LLChatMessageList,
  LLChatMessageListProps,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyMessageItemComponent(props: LLChatMessageItemProps) {
  return (
    <LLChatMessageItem
      {...props}
      MessageItemHeaderComponentStyles={headerStyle}
      MessageItemBodyComponentStyles={bodyStyle}
      MessageItemFooterComponentStyles={footerStyle}
    />
  );
}

const MyMessageListComponent = (props: LLChatMessageListProps) => {
  return (
    <LLChatMessageList
      {...props}
      MessageItemComponent={MyMessageItemComponent}
    />
  );
};

export function MyApp() {
  return (
    <LLChat
      roomId="<Your chat room id>"
      MessageListComponent={MyMessageListComponent}
    />
  );
}

const headerStyle: Partial<LLChatMessageItemHeaderStyles> = StyleSheet.create({
  avatarImage: { height: 70, width: 70 },
  username: { color: 'green' },
  ownUsername: { color: 'red' },
  timestamp: { marginTop: 10, fontSize: 9, color: 'green' },
  ownTimestamp: { marginTop: 10, fontSize: 9, color: 'red' },
});
const bodyStyle: Partial<LLChatMessageItemBodyStyles> = StyleSheet.create({
  textContainer: { margin: 10 },
});
const footerStyle: Partial<LLChatMessageItemFooterStyles> = StyleSheet.create({
  footerContainer: { marginTop: 15 },
  addReactionIcon: { height: 30, width: 30 },
});
```

#### `MessageItemMenuComponent`

| Type                                                                                                                                 | Default                                                                                                |
| :----------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| React Component of type  [LLChatMessageMenu](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageMenu) | [`LLChatMessageMenu`](https://dash.readme.com/project/livelike/v1/docs/react-native-llchatmessagemenu) |

#### `MessageItemMenuOptionComponent`

| Type                                                                                                                                            | Default                                                                                                            |
| :---------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------- |
| React Component of type [LLChatMessageMenuOption](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageMenuOption) | [`LLChatMessageMenuOption`](https://docs.livelike.com/docs/react-native-llchatmessagemenu#llchatmessagemenuoption) |

## LLChatMessageItemHeader

`LLChatMessageItemHeader` component represents the header of the message item

### Hooks used by LLChatMessageItemHeader

- [useTheme](react-native-usetheme)
- [useStyles](react-native-usestyles)

### LLChatMessageItemHeader Props

#### `message`

| Type                                                                                                                     | Default    |
| :----------------------------------------------------------------------------------------------------------------------- | :--------- |
| [IChatUserMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatUserMessage) (**Required**) | No Default |

#### `isSelfMessage`

| Type                   | Default    |
| :--------------------- | :--------- |
| boolean (**Required**) | No Default |

#### `formatMessageTimestamp`

| Type                                                   | Default                                                  |
| :----------------------------------------------------- | :------------------------------------------------------- |
| (date: string) => string.                              | Default formatter function `convertDateTime` is applied. |

#### `styles`

| Type                                                                                                                                                   | Default                                                                                                   |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLChatMessageItemHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemHeaderStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemHeader` styles. |

#### Styles Props

| CSS Class       | Type                                                         | Description                              |
| :-------------- | :----------------------------------------------------------- | :--------------------------------------- |
| headerContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Root header container                    |
| avatarImage     | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Avatar image                             |
| titleContainer  | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Container for username and and timestamp |
| username        | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Username style                           |
| ownUsername     | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Own username style                       |
| timestamp       | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Timestamp style                          |
| ownTimestamp    | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Own timestamp style                      |

## LLChatMessageItemBody

`LLChatMessageItemBody` component represents the body of the message item and renders the message text.

### Hooks used by LLChatMessageItemBody

- [useStyles](react-native-usestyles)

### LLChatMessageItemBody Props

#### `message`

| Type                                                                                                                     | Default    |
| :----------------------------------------------------------------------------------------------------------------------- | :--------- |
| [IChatUserMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatUserMessage) (**Required**) | No Default |

#### `isSelfMessage`

| Type                   | Default    |
| :--------------------- | :--------- |
| boolean (**Required**) | No Default |

#### `ChatMessageItemBodyText`

| Type                                                                                                                                                 | Default                                                                                 |
| :--------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------- |
| React Component of type  [LLChatMessageItemBodyText](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBodyText) | [`LLChatMessageItemBodyText`](react-native-llchatmessagelist#llchatmessageitembodytext) |

#### `ChatMessageItemBodyTextStyles`

[block:parameters]
{
  "data": {
    "h-0": "Type",
    "h-1": "Default",
    "0-0": "StyleSheet of type  \n[LLChatMessageItemBodyTextStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBodyTextStyles)",
    "0-1": "No Default, if present styles props would be applied on top of internal `LLChatMessageItemBodyText` styles."
  },
  "cols": 2,
  "rows": 1,
  "align": [
    "left",
    "left"
  ]
}
[/block]


#### `styles`

| Type                                                                                                                                               | Default                                                                                                 |
| :------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| StyleSheet of type [LLChatMessageItemBodyStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBodyStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemBody` styles. |

#### Styles Props

| CSS Class                | Type                                                       | Description                          |
| :----------------------- | :--------------------------------------------------------- | :----------------------------------- |
| textContainer            | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Root body container                  |
| selfMessageTextContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Root body container for self message |
| textContent              | [ViewStyle](https://reactnative.dev/docs/view-style-props) | Text content container               |

## LLChatMessageItemFooter

`LLChatMessageItemBody` represents the footer of the message item and renders the reaction picker and reaction count details as well

### Hooks used by LLChatMessageItemFooter

- [useMessageItemPopover](react-native-usemessageitempopover)
- [useReactionSpace](react-native-reaction-hooks#usereactionspace)
- [useReactionPacks](react-native-reaction-hooks#usereactionpacks)
- [useTheme](react-native-usetheme)
- [useStyles](react-native-usestyles)

### LLChatMessageItemFooter Props

#### `message`

| Type                                                                                                                        | Default    |
| :-------------------------------------------------------------------------------------------------------------------------- | :--------- |
| ## [IChatUserMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatUserMessage) (**Required**) | No Default |

#### `UserReactionsCountComponent`

| Type                                                                                                                                      | Default                                                     |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------- |
| React Component of type [LLUserReactionCounts](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCounts) | [`LLUserReactionCounts`](react-native-lluserreactioncounts) |

##### Example usage

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
  LLUserReactionCountsProps,
} from '@livelike/react-native';

function MyUserReactionsCountComponent(props: LLUserReactionCountsProps) {
  // render your custom user reactions component
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

#### `UserReactionsCountComponentStyles`

| Type                                                                                                                                             | Default                                                                                                |
| :----------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLUserReactionCountsStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLUserReactionCountsStyles) | No Default, if present styles props would be applied on top of internal `LLUserReactionCounts` styles. |

##### Example usage

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
  LLUserReactionCountsStyles,
} from '@livelike/react-native';
import { StyleSheet } from 'react-native';

function MyMessageItemFooter(props: LLChatMessageItemFooterProps) {
  return (
    <LLChatMessageItemFooter
      {...props}
      UserReactionsCountComponentStyles={userReactionsCountStyles}
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

const userReactionsCountStyles: Partial<LLUserReactionCountsStyles> =
  StyleSheet.create({
    reactionCountsContainer: { marginHorizontal: 10 },
    moreReactionsView: { backgroundColor: 'darkgrey' },
    moreReactionsText: { fontSize: 12 },
  });
```

#### `styles`

| Type                                                                                                                                                   | Default                                                                                                   |
| :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLChatMessageItemFooterStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemFooterStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemFooter` styles. |

#### Styles Props

| CSS Class       | Type                                                         | Description           |
| :-------------- | :----------------------------------------------------------- | :-------------------- |
| footerContainer | [ViewStyle](https://reactnative.dev/docs/view-style-props)   | Root footer container |
| addReactionIcon | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Add Reaction image    |

## LLChatMessageItemBodyText

The `LLChatMessageItemBodyText`component renders the message body content. It can be a text, gif or sticker.

### Hooks used by LLChatMessageItemBodyText

- [useStickerPacks](react-native-usestickerpacks)
- [useStyles](react-native-usestyles)

### LLChatMessageItemBodyText Props

#### `message`

| Type                                                                                                                     | Default    |
| :----------------------------------------------------------------------------------------------------------------------- | :--------- |
| [IChatUserMessage](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=IChatUserMessage) (**Required**) | No Default |

#### `isDeleted`

| Type    | Default    |
| :------ | :--------- |
| boolean | No Default |

#### `isSelfMessage`

| Type    | Default    |
| :------ | :--------- |
| boolean | No Default |

#### `styles`

| Type                                                                                                                                                       | Default                                                                                                     |
| :--------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| StyleSheet of type [LLChatMessageItemBodyTextStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageItemBodyTextStyles) | No Default, if present styles props would be applied on top of internal `LLChatMessageItemBodyText` styles. |

#### Styles Props

| CSS Class          | Type                                                         | Description                             |
| :----------------- | :----------------------------------------------------------- | :-------------------------------------- |
| text               | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Message text styles                     |
| deletedMessageText | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Message text for deleted message styles |
| selfMessageText    | [TextStyle](https://reactnative.dev/docs/text-style-props)   | Message text for self message styles    |
| stickerImage       | [ImageStyle](https://reactnative.dev/docs/image-style-props) | Message sticker image styles            |