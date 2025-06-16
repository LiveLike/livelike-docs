---
title: LLChat
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
      slug: react-native-llchatmessagelist
      title: LLChatMessageList
    - type: basic
      slug: react-native-llchatmessagecomposer
      title: LLChatMessageComposer
    - type: basic
      slug: react-native-llchatheader
      title: LLChatHeader
    - type: basic
      slug: react-native-llchatbanner
      title: LLChatBanner
---
`LLChat` is the main Chat UI component that renders the chat room UI with a chat header, message list, message composer and chat banner.

> 🚧 Pre-requisite
>
> Make sure you [initialise the SDK](react-native-getting-started#initialise-react-native-sdk).

```text react native
import { LLChat } from '@livelike/react-native'

export function MyChat(){
	return <LLChat roomId="xxx-yyy-zzz-www-vvv"/>
}
```

> 👍 Snack Expo playground
>
> Refer [LLChat](https://snack.expo.dev/@aquibv/livelike-chat) snack expo playground

## Hooks used by `LLChat`

* [useChatRoom](react-native-usechatroom)
* [useLoadStickerPacksEffect] \(react-native-useloadstickerpackseffect)
* [useStyles](react-native-usestyles)

## `LLChat` component hierarchy:

<Image align="center" width="smart" src="https://files.readme.io/fbb69eb-LLChat-comp-heirarchy.png" />

## LLChat Props

> 📘 Customisation Core concept
>
> Refer [customisation](react-native-customisation) core concepts to understand different level of component customisation that could be achieved through below mentioned props.

#### `roomId`

| Type                  | Default    |
| :-------------------- | :--------- |
| String (**Required**) | No Default |

This is the room Id of the chat (that you can get from the producer suite). In case of dynamic chat room, you can use [`getChatRooms`](javascript-chat-rooms#get-available-chat-rooms) JS API to fetch all chat rooms in an application.

#### `userAvatarUrl`

| Type   | Default    |
| :----- | :--------- |
| String | No Default |

This property allows integrators to set avatars for the LLChat component by providing an avatar image URL. To set a custom avatar for an `LLChat` instance, use the `userAvatarUrl` property and provide the URL of the desired avatar image. Here's an example of how to use it:

```javascript react-native
<LLChat
  roomId="xxx-yyy-zzz-www-vvv"
  userAvatarUrl='https://example.com/avatar.png'
/>
```

#### `styles`

| Type                                                                                              | Default                                                                                                                                            |
| :------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| [LLChatStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatStyles) | No Default, if present styles props would be applied on top of internal styles of type [LLChatStyles](react-native-llchat#llchatstyles-stylesheet) |

##### `LLChatStyles` stylesheet

| Stylesheet prop name | Description                                                               |
| :------------------- | :------------------------------------------------------------------------ |
| `chatContainer`      | Chat view container styles. This container wraps all the chat components. |

#### `HeaderComponent`

| Type                                                                                                                      | Default                                     |
| :------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------ |
| React Component of type [LLChatHeader](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatHeader) | [`LLChatHeader`](react-native-llchatheader) |

Rendered at the top of the Chat UI. This prop could be used to pass your custom `HeaderComponent`

##### Example usage:

```typescript
import { LLChat, LLChatHeaderProps } from '@livelike/react-native';

function MyChatHeader(props: LLChatHeaderProps) {
  // render your custom chat header
}

export function MyApp() {
  return <LLChat roomId="<Your chat room id>" HeaderComponent={MyChatHeader} />;
}
```

#### `HeaderComponentStyles`

| Type                                                                                                          | Default                                                                                                                          |
| :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------- |
| [LLChatHeaderStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatHeaderStyles) | No Default, if present styles props would be applied on top of internal  [LLChatHeader styles](react-native-llchatheader#styles) |

HeaderComponent styles prop which could be used to modify styles of default rendered `LLChatHeader` component.

#### `BannerComponent`

| Type                                                                                                                      | Default                                     |
| :------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------ |
| React component of type [LLChatBanner](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBanner) | [`LLChatBanner`](react-native-llchatbanner) |

`BannerComponent` is rendered in response to any moderation based action for eg Reporting a message, deleting a message or blocking a profile.\
This prop could be used to pass your custom Banner Component.

##### Example usage:

```typescript
import { LLChat, LLChatBannerProps } from '@livelike/react-native';

function MyChatBanner(props: LLChatBannerProps) {
  // render your custom chat banner
}

export function MyApp() {
  return <LLChat roomId="<Your chat room id>" BannerComponent={MyChatBanner} />;
}
```

#### `BannerComponentStyles`

| Type                                                                                                          | Default                                                                                                                         |
| :------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------ |
| [LLChatBannerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatBannerStyles) | No Default, if present styles props would be applied on top of internal [LLChatBanner styles](react-native-llchatbanner#styles) |

BannerComponent styles prop which could be used to modify styles of default rendered `LLChatBanner` component.

#### `MessageListComponent`

| Type                                                                                                                                | Default                                               |
| :---------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------- |
| React Component of type [LLChatMessageList](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageList) | [`LLChatMessageList`](react-native-llchatmessagelist) |

Rendered as the chat message list. This prop could be used to pass your custom message list component. Internally we render `FlatList` component from `react-native`. In case there's need of customising default rendered message item, use this prop to pass your custom message item component

##### Example usage:

```typescript
import {
  LLChat,
  LLChatMessageList,
  LLChatMessageListProps,
  LLChatMessageItemProps,
} from '@livelike/react-native';

function MyListItem(props: LLChatMessageItemProps) {
  // render your custom message item prop
}
function MyList(props: LLChatMessageListProps) {
  return <LLChatMessageList {...props} />;
}

export function MyApp() {
  return <LLChat roomId="<Your chat room id>" MessageListComponent={MyList} />;
}
```

#### `MessageListComponentStyles`

| Type                                                                                                                    | Default                                                                                                                                   |
| :---------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| [LLChatMessageListStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageListStyles) | No Default, if present styles props would be applied on top of internal [LLChatMessageList styles](react-native-llchatmessagelist#styles) |

MessageListComponent styles prop which could be used to modify styles of default rendered `LLChatMessageList` component.

#### `MessageComposerComponent`

| Type                                                                                                                                        | Default                                                       |
| :------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------ |
| React Component of type [LLChatMessageComposer](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageComposer) | [`LLChatMessageComposer`](react-native-llchatmessagecomposer) |

Rendered at the bottom of the Chat UI. This prop could be used to pass your custom composer component. This component renders:

* `TextInput` - To send a text message.
* `Sticker Picker` - To pick and send sticker image message
* `Gif Picker` - To pick and send gif message.

##### Example usage:

```typescript
import { LLChat, LLChatMessageComposerProps } from '@livelike/react-native';

function MyComposer(props: LLChatMessageComposerProps) {
  // render your custom composer component
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

#### `MessageComposerComponentStyles`

| Type                                                                                                                            | Default                                                                                                                                           |
| :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------ |
| [LLChatMessageComposerStyles](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=LLChatMessageComposerStyles) | No Default, if present styles props would be applied on top of internal [LLChatMessageComposer styles](react-native-llchatmessagecomposer#styles) |

Message composer component styles prop which could be used to modify styles of default rendered `LLChatMessageComposer` component.
