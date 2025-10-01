---
title: Reaction Hooks
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Reaction hooks are the set of hooks which would enable you to use Reactions for any entity that could be reacted upon.

> 📘 What are Reactions?
>
> Refer our core [reactions](reactions)  documentation

## useReactionSpace

`useReactionSpace` hook gives you reaction space state based on given `targetGroupId`. 

**Hook Type definition**: [useReactionSpace](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useReactionSpace)

##### Example Usage:

```typescript
import { useReactionSpace } from "@livelike/react-native";

const { reactionSpace } = useReactionSpace({
  targetGroupId: "<Target group ID>",
});
```

## useReactionPacks

`useReactionPacks` gives you list of reaction pack that are mapped with a given a reaction space. You need a reaction space Id for this hook that could be retrieved using [useReactionSpace](reaction-hooks#useReactionSpace).

For loading reaction pack state and keeping the state update, you need to use  [useLoadReactionPacksEffect](react-native-reaction-hooks#useloadreactionpackseffect) hook.

**Hook Type definition**: [useReactionPacks](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useReactionPacks)

##### Example Usage:

```typescript
import { useReactionSpace, useReactionPacks } from "@livelike/react-native";

const { reactionSpace } = useReactionSpace({
  targetGroupId: "<Target group ID>",
});
const { reactionPacks } = useReactionPacks({
  reactionSpaceId: reactionSpace?.id,
});
```

## useLoadReactionPacksEffect

`useLoadReactionPacksEffect` hook loads the reaction packs state and also updates the reaction packs state for any change made in the reaction packs through our producer suite.

**Hook Type definition**: [useLoadReactionPacksEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useLoadReactionPacksEffect)

##### Example Usage:

```typescript
import { useReactionSpace, useLoadReactionPacksEffect } from "@livelike/react-native";

const { reactionSpace } = useReactionSpace({ targetGroupId: "<Room ID>" });
useLoadReactionPacksEffect({ reactionSpaceId: reactionSpace?.id });
```

## useUserReactions

`useUserReactions` hook returns user reactions state for multiple targets. You need a reaction space Id for this hook that could be retrieved using [useReactionSpace](reaction-hooks#useReactionSpace)\
For loading user reactions state, use [useLoadUserReactions](react-native-useloaduserreactions) hook.

For auto updating user reactions state whenever any user adds or removes reaction, use [useUserReactionEffect](react-native-useuserreactioneffect)

**Hook Type definition**: [useUserReactions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useUserReactions)

##### Example Usage:

```typescript
import { useMemo } from "react";
import { 
  useReactionSpace,
  useLoadUserReactions,
  useReactions,
  useChatMessages
} from "@livelike/react-native";

const { reactionPacks, reactionSpace } = useReactions({
  targetGroupId: "<Room ID>",
});

const { messages } = useChatMessages({ roomId: "<Room ID>" });
const targetIds = useMemo(() => messages.map(({ id }) => id), [messages]);

const { userReactions } = useUserReactions({
  reactionSpace,
  targetIds,
});
```

## useLoadUserReactions

`useLoadUserReactions` hook is to load user reactions state. You need a reaction space Id for this hook that could be retrieved using [useReactionSpace](reaction-hooks#useReactionSpace)\
This hook implements a lazy load technique. To fetch the resources you need to invoke the `loadUserReactions` function that is returned by this hook.

**Hook Type definition**: [useLoadUserReactions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useLoadUserReactions)

##### Example Usage:

```typescript
import { useReactionSpace, useLoadUserReactions } from "@livelike/react-native";

const { reactionSpace } = useReactionSpace({ targetGroupId: "<your entity Id>" });
const { loadUserReactions } = useLoadUserReactions({
  reactionSpaceId: reactionSpace?.id,
});

const targetIds = useMemo(() => messages.map(({ id }) => id), [messages]);
useEffect(() => {
  if (!targetIds.length) {
    return;
  }
  loadUserReactions({ targetIds });
}, [targetIds]);
```

## useUserReactionEffect

`useUserReactionEffect` is a side effect based hook that updates user reactions state whenever any user adds or removes reactions. This hook makes user reaction state reactive keeping it up to date with latest user reactions. Internally it uses reaction space event listeners to listen to `ADD_REACTION` and `REMOVE_REACTION` event.\
Make sure to use this hook only once in your react component tree.

You need a reaction space Id for this hook that could be retrieved using [useReactionSpace](reaction-hooks#useReactionSpace)  

**Hook Type definition**: [useUserReactionEffect](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useUserReactionEffect)

##### Example Usage:

```typescript
import { useReactionSpace, useUserReactionEffect } from "@livelike/react-native";

const { reactionSpace } = useReactionSpace({ targetGroupId: "<Room ID>" });
useUserReactionEffect({ reactionSpaceId: reactionSpace?.id });
```

## useUserReactionActions

The `useUserReactionActions` hook is designed to handle user reactions, providing functions that are executed when a user adds or removes reactions. This is useful for managing interactive features where users can express their sentiments or opinions through reactions.

You need a reaction space Id for this hook that could be retrieved using [useReactionSpace](reaction-hooks#useReactionSpace)

**Hook Type definition**: [useUserReactionActions](https://livelike-doc-redirect-url.herokuapp.com/react-native?keyword=useUserReactionActions)

##### Example usage:

The useUserReactionActions hook is used to initialize functions for handling user reactions. It returns an object with functions (addReaction and removeReaction) that you can use to manage user reactions.

```typescript
import { useUserReactionActions } from "@livelike/react-native";

const { addReaction, removeReaction } = useUserReactionActions({ targetGroupId: "<Room ID>", targetId: "<Message ID>" });
const { userReactions } = useUserReactions({
  reactionSpaceId,
  targetId,
});
const selfReactionId = userReactions?.[reactionId]?.self_reacted_user_reaction_id;
const actionArgs = {
  reactionSpaceId: reactionSpace?.id,
  userReaction: {
    target_id: targetId,
    reaction_id: reactionId,
    reacted_by_id: userProfile.id,
    id: DUMMY_USER_REACTION_ID,
  }
  profileId: userProfile.id,
}
addReaction(actionArgs);
removeReaction(actionArgs, selfReactionId)

```
