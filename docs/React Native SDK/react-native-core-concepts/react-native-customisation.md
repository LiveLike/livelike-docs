---
title: Customisation
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
      slug: react-native-custom-hooks
      title: Custom hooks
---
We believe in seamless integration experience but we also know that every client has their own way of developing apps by managing UI state with their own business logic and would have their own UX design. Therefore we want to provide different level of customisation which you could choose from based on your level of time and efforts needed to drive your business needs. 
[block:api-header]
{
  "title": "Theme Customisation"
}
[/block]
You could customise dark and light theme colors to match your App design system. Use `setThemes` function provided by `useTheme` hook to set your custom theme.

#### Example:
Setting custom dark and light theme  
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0e7b343-theme-customisation.png",
        "theme-customisation.png",
        2349,
        2346,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import React, { useCallback, useMemo, useLayoutEffect } from 'react';\nimport {\n  StyleSheet,\n  Text,\n  View,\n  Platform,\n  ActivityIndicator,\n  Image,\n  TouchableOpacity,\n} from 'react-native';\nimport {\n  useInit,\n  LLChat,\n  useTheme,\n  LLThemeType,\n  LLChatHeaderProps,\n  useStyles,\n  LLThemes,\n} from '@livelike/react-native';\nimport ThemeLight from './assets/theme-light.png';\nimport ThemeDark from './assets/theme-dark.png';\n\nconst myCustomTheme: LLThemes = {\n  [LLThemeType.DARK]: {\n    text: '#ffff',\n    secondaryText: '#A3C7D6',\n    background: '#0A2647',\n    secondaryBackground: '#144272',\n    thirdBackground: '#144272',\n    popoverBackground: '#2C74B3',\n    inputBackground: '#144272',\n    primaryButtonBackground: '#2C74B3',\n    border: '#BBE1FA',\n    info: '#4ECCA3',\n    error: '#EB455F',\n  },\n  [LLThemeType.LIGHT]: {\n    text: '#000',\n    secondaryText: '#65647C',\n    background: '#F8EDE3',\n    secondaryBackground: '#DFD3C3',\n    thirdBackground: '#DFD3C3',\n    popoverBackground: '#D0B8A8',\n    inputBackground: '#F8EDE3',\n    primaryButtonBackground: '#85586F',\n    border: '#85586F',\n    info: '#4ECCA3',\n    error: '#EB455F',\n  },\n};\n\nexport default function App() {\n  const { profile, loaded } = useInit({\n    clientId: '<Your App client Id>',\n  });\n  const { setThemes } = useTheme();\n\n  const appStyles = useStyles({\n    componentStylesFn: stylesFn,\n  });\n  \n  useLayoutEffect(() => {\n    setThemes(myCustomTheme);\n  }, []);\n\n  if (!loaded) {\n    return (\n      <ActivityIndicator style={{ display: 'flex', flex: 1 }} size={'large'} />\n    );\n  }\n\n  if (!profile) {\n    return <Text style={appStyles.errorContainer}>Error loading profile</Text>;\n  }\n\n  return (\n      <LLChat\n        roomId=\"<Your Chat room Id>\"\n      />\n  );\n}\n",
      "language": "typescript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "UI Customisation"
}
[/block]
Using React Native SDK, based on your business requirement and based on your level of customisation efforts there could be 4 ways to achieve it:

1. Stock UI.
2. Stock UI + custom Presentational Component. 
3. Hooks + custom Component.
4. JS API + custom UI.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3fcd941-TimeVsEfforts.png",
        "TimeVsEfforts.png",
        1620,
        1311,
        "#000000"
      ],
      "caption": "Customisation Time vs Effort",
      "sizing": "smart"
    }
  ]
}
[/block]
Let us try to understand these customisation in detail.

### 1. Stock UI:

This is the simplest and easiest way to integrate LiveLike Stock UI components requiring less efforts and time. Our stock UI offers:
* Highly customisable and themeable UI for most of our LiveLike services.
* Abstract out the UI implementation and state management complexity.  
* Out of box seamless integration experience.
You could start integrating React native components using this option and gradually move towards 2nd option.
#### Example:
Lets say you want to integrate LiveLike chat community service, you could import `LLChat` and pass `roomId` required prop.
[block:callout]
{
  "type": "warning",
  "title": "Need to initialise the SDK",
  "body": "Before rendering or using any functionalities from React Native SDK, make sure to [initialise the SDK](react-native-getting-started#initialise-react-native-sdk)"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cf0c007-StockUI-example.png",
        "StockUI-example.png",
        2349,
        2346,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport { ActivityIndicator } from 'react-native';\nimport { useInit, LLChat } from '@livelike/react-native';\n\nexport default function App() {\n  const { loaded } = useInit({\n    clientId: '<Your App client Id>',\n  });\n\n  if (!loaded) {\n    return <ActivityIndicator />;\n  }\n\n  return <LLChat roomId=\"<Your Chat room Id>\" />;\n}",
      "language": "typescript"
    }
  ]
}
[/block]
This render a complete Chat UI with a chat header, message list and a chat message composer, user reaction and moderation capabilities.

 
### 2. Stock UI + Custom Presentational Component:

This way of customisation would require less time but more efforts than 1st option. This could be your preferred way if the Stock UI implementation suffice your business needs but you just want to customise the smaller fraction of presentational part of the UI based on your application UX design. Our container components accepts two props with which you could customise the presentational part.
##### a.  `XXXXYYYYComponent` prop:
This lets you to pass your own custom component needed to be rendered by a given a component with the help of which you could completely customise the UI. For more details on what props would be passed to your rendered custom component, refer the corresponding component documentation.
##### b. `XXXXYYYYStyle` prop:
This lets you tweak or change styles of child component for a given component for eg: adjust padding, change color, font size etc. Use `Stylesheet.create` API from `react-native` package to create styles object and to identify the needed style object properties, refer the corresponding component documentation. Usually all our component exports a `XXXXYYYYStyles` TS type which could be used to type this `styles` prop.

This prop design pattern is similar to React Native components for eg: [`FlatList`](https://reactnative.dev/docs/flatlist#listheadercomponent) 
  
#### Example 1:
Taking above same example of rendering a chat UI, suppose your business requirement is to conditionally render composer component for an influencer chat where for non influencer there should not be any composer rendered.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b1eac4a-CustomPresentation.png",
        "CustomPresentation.png",
        2349,
        2346,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import React, { useMemo } from 'react';\nimport { ActivityIndicator } from 'react-native';\nimport {\n  useInit,\n  LLChat,\n  LLChatMessageComposerProps,\n  LLChatMessageComposer,\n} from '@livelike/react-native';\n\nexport function MyComposer(props: LLChatMessageComposerProps) {\n  // assuming a hook which parses userProfil.custom_data value\n  // and returns isInfluencer which was set using updateUserProfile JS API\n  const isInfluencer = useIsInfluencer();\n  if (isInfluencer) {\n    return <LLChatMessageComposer {...props} />;\n  }\n  return null;\n}\n\nexport default function App() {\n  const { loaded } = useInit({\n    clientId: '<Your App client Id>',\n  });\n\n  if (!loaded) {\n    return <ActivityIndicator />;\n  }\n\n  return (\n    <LLChat\n      roomId=\"<Your Chat room Id>\"\n      MessageComposerComponent={MyComposer}\n    />\n  );\n}",
      "language": "typescript"
    }
  ]
}
[/block]
As seen in the code snippet example, passing `ChatMessageComposerComponent` prop as `MyComposer` component, renders no composer for normal userprofile and it would render `LLChatMessageComposer` for influencer profile.  

#### Example 2:
Lets assume you want to change padding and background of list component and add top padding to chat header. This could be achieved by passing a custom header and message list styles prop. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d430948-Custom-styles.png",
        "Custom-styles.png",
        2349,
        2346,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import React from 'react';\nimport { StyleSheet, ActivityIndicator } from 'react-native';\nimport {\n  useInit,\n  LLChat,\n  LLChatMessageListProps,\n  LLChatMessageList,\n  LLChatMessageListStyles,\n  LLChatHeader,\n  LLChatHeaderProps,\n  LLChatHeaderStyles,\n  useTheme,\n} from '@livelike/react-native';\n\nexport default function App() {\n  const { loaded } = useInit({\n    clientId: '<Your App client Id>',\n  });\n  const { themeType } = useTheme();\n  const messageListStyles = useMemo(() => messageListStylesFn(themeType), [themeType]);\n\n  if (!loaded) {\n    return <ActivityIndicator />;\n  }\n  \n  return (\n    <LLChat\n      roomId=\"<Your Chat room Id\"\n      HeaderComponentStyle={hearderStyles}\n      MessageListComponentStyle={messageListStyles}\n    />\n  );\n}\n\nconst messageListStylesFn: (\n  theme: 'light' | 'dark'\n) => Partial<LLChatMessageListStyles> = (theme) =>\n  StyleSheet.create({\n    rootContainer: {\n      padding: 20,\n      backgroundColor: theme === 'light' ? '#A0C3D2' : '#2b4956',\n    },\n  });\n\nconst hearderStyles: Partial<LLChatHeaderStyles> = StyleSheet.create({\n  headerTitle: {\n    paddingTop: 50,\n  },\n});",
      "language": "typescript"
    }
  ]
}
[/block]
### 3. Hooks + custom Component

This way of customisation lets you drive your own UI implementation completely in case your UX design is different than default stock UI. 
Usually the need of this customisation would be when the UI state logic suffices your business needs but the component layout, component hierarchy and the rendered UI components is different than default stock UI where by using 2nd option (i.e using `XXXXYYYComponent` and `XXXYYYYStyle` props) you end up passing custom presentational component at each and every level. In this case driving your own custom UI would simplify your implementation and make it more manageable & scalable.
You could use our exported hooks that manages UI state for our Stock UI.

#### Example:
Taking same earlier example of rendering Chat UI, you could use `useChatRoom` and `useChatMessages` to render chat room details, message list and message composer.  
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/387ed55-HookCustom_UI.png",
        "Hook+Custom UI.png",
        2349,
        2334,
        "#000000"
      ],
      "sizing": "smart"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import React, { useState } from 'react';\nimport {\n  ActivityIndicator,\n  View,\n  Text,\n  FlatList,\n  TextInput,\n  Button,\n  StyleSheet,\n  Platform,\n  TouchableOpacity,\n} from 'react-native';\nimport { useInit, useChatRoom, useChatMessages } from '@livelike/react-native';\n\nexport default function CustomApp() {\n  const { loaded } = useInit({\n    clientId: '<Your App client Id>',\n  });\n\n  if (!loaded) {\n    return <ActivityIndicator />;\n  }\n\n  return <MyChat roomId=\"<Your Chat room Id\" />;\n}\n\nconst listItemKeyExtractor = (message) => message.id;\n\nfunction MyChatMessageItem({ message: messageDetails }) {\n  return (\n    <View style={appStyles.messageListItem}>\n      <Text>{messageDetails.message}</Text>\n    </View>\n  );\n}\n\nfunction MyChat({ roomId }: { roomId: string }) {\n  // using useChatRoom hook to get chat room data\n  const { chatRoom } = useChatRoom({ roomId });\n  // using useChatMessages hook to get live message list and sendMessage function\n  const { sendMessage, messages } = useChatMessages({ roomId });\n  const [inputValue, setInputValue] = useState('');\n\n  if (!chatRoom) {\n    return <ActivityIndicator size={'large'} />;\n  }\n\n  return (\n    <View style={appStyles.chatContainer}>\n      <Text style={appStyles.chatHeader}>{chatRoom.title}</Text>\n      <FlatList\n        style={appStyles.messageList}\n        data={messages}\n        renderItem={({ item }) => <MyChatMessageItem message={item} />}\n        keyExtractor={listItemKeyExtractor}\n      />\n      <View style={appStyles.composer}>\n        <TextInput\n          onChangeText={setInputValue}\n          value={inputValue}\n          style={appStyles.chatInput}\n          placeholder=\"Enter message\"\n          placeholderTextColor={'gray'}\n        />\n        <TouchableOpacity\n          style={appStyles.sendButton}\n          onPress={() =>\n            sendMessage({ message: inputValue, roomId }).finally(() => {\n              setInputValue('');\n            })\n          }\n        >\n          <Text style={appStyles.sendButtonText}>Send</Text>\n        </TouchableOpacity>\n      </View>\n    </View>\n  );\n}\n\nconst appStyles = StyleSheet.create({\n  chatContainer: {\n    display: 'flex',\n    flexDirection: 'column',\n    flex: 1,\n    padding: 15,\n    backgroundColor: '#EAE7B1',\n  },\n  chatHeader: {\n    marginTop: Platform.OS === 'ios' ? 50 : 20,\n    height: 30,\n    display: 'flex',\n    alignItems: 'center',\n    justifyContent: 'center',\n    width: '100%',\n    textAlign: 'center',\n  },\n  messageList: {\n    flex: 2,\n    minHeight: 300,\n    width: '100%',\n  },\n  messageListItem: {\n    display: 'flex',\n    padding: 10,\n    margin: 7,\n    borderRadius: 5,\n    backgroundColor: '#A6BB8D',\n  },\n  composer: {\n    display: 'flex',\n    flexDirection: 'row',\n  },\n  chatInput: {\n    flex: 1,\n    height: 40,\n    padding: 5,\n    borderRadius: 5,\n    backgroundColor: '#A6BB8D',\n    marginRight: 10,\n  },\n  sendButton: {\n    backgroundColor: '#3C6255',\n    display: 'flex',\n    justifyContent: 'center',\n    width: 60,\n    alignItems: 'center',\n  },\n  sendButtonText: {\n    color: '#FFFF',\n  },\n});\n",
      "language": "typescript"
    }
  ]
}
[/block]
### 4. JS API + Custom UI

This way of customisation lets you drive your own business logic to manage UI state in your own preferred way and render your own custom UI. This could be useful for an application owners who wants to gradually adopt LiveLike services in their existing app ecosystem where they already have their own UI state management and their own UX design. If needed you could still use our presentational components passing needed props to render the component.
##### JS API are part of Javascript package, so any JS API to be used are to be imported from `@livelike/javascript` package. 

#### Example:
Taking same earlier example of rendering Chat UI, suppose you already have Redux as your React state management. You could use `getChatroom` and `getMessageList` JS API to load chat room details and message list in your state.  
[block:code]
{
  "codes": [
    {
      "code": "import { useEffect } from 'react';\nimport { getChatRoom, getMessageList } from '@livelike/javascript';\nimport { useDispatch, useSelector } from 'react-redux';\n\nconst initialState = {\n  chatRoomDetails: undefined,\n  chatMessages: [],\n};\n\n// assuming redux thunk is configured as middleware, this is a thunk function\n// for loading side effects\nexport async function fetchChatRoomResources({ roomId }) {\n  return async function fetchChatRoomThunk(dispatch, getState) {\n    const responses = Promise.all([\n      getChatRoom({ roomId }),\n      getMessageList(roomId),\n    ]);\n    dispatch({\n      type: 'chat/chatroomResources',\n      payload: {\n        chatRoomDetails: responses[0],\n        chatMessages: responses[1],\n      },\n    });\n  };\n}\n\nexport async function fetchMessages({ roomId }) {\n  return async function fetchMessagesThunk(dispatch, getState) {\n    const { messages } = await getMessageList(roomId);\n    dispatch({ type: 'chat/chatRoom', payload: messages });\n  };\n}\n\nexport function MyChat({ roomId }) {\n  const dispatch = useDispatch();\n  const chatRoom = useSelector((state) => state.chatRoomDetails);\n  const messages = useSelector((state) => state.chatMessages);\n  useEffect(() => {\n    dispatch(fetchChatRoomResources({ roomId }));\n  }, []);\n\n  return (\n    <>\n      {\n        // Your own custom Chat UI\n      }\n    </>\n  );\n}",
      "language": "typescript"
    }
  ]
}
[/block]