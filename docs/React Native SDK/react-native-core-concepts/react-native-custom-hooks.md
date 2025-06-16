---
title: Custom hooks
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
      slug: react-native-components
      title: Components
---
We provide a set of custom hooks which could be categorised based on their objective and functionalities. 
[block:api-header]
{
  "title": "1. Resource based hooks:"
}
[/block]
The purpose of these hooks is to provide you UI state or reactive resources which could be used by UI components. These resources could be:
* UI specific states - eg: UI state flag which drives showing or hiding gif picker.
* LiveLike resource entity - eg: LiveLike chat messages, reaction packs, sticker packs, reaction space, user reactions, widgets etc.
Few examples of resource based hooks are:
* `useChatRoom`
* `useChatMessages`
* `useReactionPacks`
* `useReactionPacks`
* `useStickerPicker`
* `useGifPicker`

[block:api-header]
{
  "title": "2. Side effect based hooks:"
}
[/block]
These hooks when invoked either introduces some side effects which in turn drives UI state resources or provide an API for you to manually drive such side effect. This side effects could either be creating subscriptions to update resources or initial loading of resources. Mostly these hooks would be invoked once per UI lifecycle based on its dependencies and thus we recommend to use these side effect hook at the top level of your UI component hierarchy. To identify side effect based hook, we suffix the hook name with `effect`. 
For example:
* `useChatMessagesEffect` -> Based on provided `roomId`, this hook subscribes to Livelike channels for updating chat message list resource in real time. Since its a subscription side effect, we recommend invoking `useChatMessagesEffect` at the top level component to have minimum subscriptions and unsubscriptions. 
* `useLoadReactions` -> Based on provided `reactionSpaceId`, this hooks fetches and updates reaction pack resource.
* `useUserReactionEffect`-> Based on provided `reactionSpaceId`, this hook subscribes to Reaction space channel for updating user reaction state resources.

[block:api-header]
{
  "title": "3. Action based hooks:"
}
[/block]
These hooks exports action handlers or API which could be used by UI component to update the state resources. More or less its like `setState` based API functions.
Few examples of action based hooks:
* `useChatMessageActions`-> returns `sendChatMessage` and `deleteChatMessage` action handlers that add and remove a chat message from the chat message list resource respectively. 
* `useBannerActions` -> returns `addBannerItem` action handler that add a banner item to `banners` list.