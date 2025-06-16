---
title: Common Web Solutions
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Solutions

1. Initialization

   - [Loading SDK as script](#loading-sdk-as-script)
   - [Loading SDK as Node Module](#loading-sdk-as-node-module)
   - [Minimum initialization](#minimum-initialization)
   - [Accessing profile from initialization](#accessing-profile-from-initialization)
   - [Initialization with logger active](#initialization-with-logger-active)
   - [Initialization with custom translations](#initialization-with-custom-translations)
   - [Initialization with custom theme](#initialization-with-custom-theme)
   - [Initializing with profile access token](#initializing-with-profile-access-token)
   - [Initializing with custom profile nickname](#initializing-with-custom-profile-nickname)
   - [Updating profile nickname after initialization](#updating-profile-nickname-after-initialization)
   - [Initializing with loaded accessToken](#initializing-with-loaded-accessToken)
   - [Initializing with loaded accessToken and ensuring nicknames match](#initializing-with-loaded-accessToken-and-ensuring-nicknames-match)
   - [Ensuring LiveLike SDK is loaded without Promises](#ensuring-livelike-sdk-is-loaded-without-promises)

2. Profile

   - [Getting Profile](#getting-profile)
   - [Updating Profile](#updating-profile)

3. Widgets

   - [Creating a custom pop-up mode](#Creating-a-custom-pop-up-mode)
   - [Creating a custom mode where widgets are interactive indefinitely](#creating-a-custom-mode-where-widgets-are-interactive-indefinitely)
   - [Creating a custom timeline mode](#Creating-a-custom-timeline-mode)
   - [Creating a custom widget mode with animations](#Creating-a-custom-widget-mode-with-animations)
   - [Set widget theme styles](#set-widget-theme-styles)
   - [Set widget translations](#set-widget-translations)
   - [Add sounds to widget interactions](#add-sounds-to-widget-interactions)
   - [Displaying a single widget HTML tag](#displaying-a-single-widget-html-tag)
   - [Displaying a previews widget](#displaying-a-preview-widget)
   - [Creating widget element programmatically](#creating-widget-element-programmatically)
   - [Creating widget element programmatically with custom mode](#creating-widget-element-programmatically-with-custom-mode)
   - [Creating custom widget template](#creating-custom-widget-template)

## SDK Initialization

### Loading SDK as script

```html
<script src="https://unpkg.com/@livelike/engagementsdk@2.8.3/livelike.umd.js"></script>
```

### Loading SDK as Node Module

```js
import LiveLike from "@livelike/engagementsdk";
```

### Minimum initialization

```js
LiveLike.init({ clientId: "<your-client-id>" });
```

### Accessing profile from initialization

```js
LiveLike.init({ clientId: "<your-client-id>" }).then((profile) =>
  console.log(profile)
);
```

### Initialization with logger active

```js
LiveLike.init({ clientId: "<your-client-id>", logger: true });
```

### Initialization with custom translations

```js
LiveLike.init({
  clientId: "<your-client-id>",
  localizedStrings: {
    en: {
      "chat.inputPlaceholder": "Send message",
    },
    es: {
      "chat.inputPlaceholder": "Enviar mensaje",
    },
  },
});
```

### Initialization with custom theme

```js
LiveLike.init({
  clientId: "<your-client-id>",
  theme: {
    widgets: {
      poll: {
        header: {
          background: { format: "fill", color: "#0000ff" },
        },
        selectedOptionDescription: {
          fontColor: "#000000",
        },
      },
      quiz: {
        header: {
          background: { format: "fill", color: "#ff0000" },
        },
      },
    },
  },
});
```

### Initializing with profile access token

```js
LiveLike.init({
  clientId: "<your-client-id>",
  accessToken: "<your-access-token>",
});
```

### Initializing with custom profile nickname

```js
LiveLike.init({
  clientId: "<your-client-id>",
  nickName: "<your-nick-name>",
});
```

**Note:** The custom nickname will only apply to the user profile if the profile is being created. A new profile is created only when it's the first time a user is loading the application.

### Updating profile nickname after initialization

```js
const newNickname = "New Nickname";

LiveLike.init({ clientId: "<your-client-id>" }).then(
  (profile) =>
    profile.nickname !== newNickname &&
    LiveLike.updateUserProfile({
      accessToken: profile.access_token,
      options: { nickname: newNickname },
    })
);
```

### Initializing with loaded accessToken

```js
fetchSavedUserProfile().then((savedProfile) =>
  LiveLike.init({
    clientId: "<your-client-id>",
    accessToken: savedProfile.access_token,
  }).then(
    (livelikeProfile) =>
      !savedProfile.access_token && saveUserProfile(livelikeProfile)
  )
);
```

**Note: ** The `fetchSavedUserProfile` function is a placeholder for one of your functions that will fetch your saved user profile.

The `saveUserProfile` function is a placeholder for one of your functions that will save the LiveLike profile to your backend, localStorage, etc.

If your saved user profile contains an access_token, it will be used to initialize the application, and the correct LiveLike profile will be loaded.

If you saved user profile does not contain an access_token, the LiveLike profile is saved.

### Initializing with loaded accessToken and ensuring nicknames match

```js
fetchSavedUserProfile().then((savedProfile) =>
  LiveLike.init({
    clientId: "<your-client-id>",
    accessToken: savedProfile.access_token,
    nickname: savedProfile.nickname,
  }).then((livelikeProfile) => {
    if (!savedProfile.access_token) {
      saveUserProfile(livelikeProfile);
    }
    if (livelikeProfile.nickname !== savedProfile.nickname) {
      LiveLike.updateUserProfile({
        accessToken: livelikeProfile.access_token,
        options: { nickname: newNickname },
      });
    }
  })
);
```

**Note:** This is meant to ensure your saved user profile is up to date with LiveLike's profile's accessToken, and that your saved profile's nickname matches LiveLike's profile's nickname.

1. If your saved profile contains an access token, it will use that to load the correct LiveLike profile.

2. If it does not contain an access token, but it does contain a nickname, it uses that to create a new LiveLike profile with that nickname.

3. If your saved profile does not contain an access token, it saves LiveLike's profile to use the accessToken in subsequent application loads.

4. If your saved profile's nickname does not match LiveLike's profile's nickname, the profile is updated with the matching nickname.

## Ensuring LiveLike SDK is loaded without Promises

```js
LiveLike.init({ clientId: "<your-client-id>" });

function hasLiveLikeLoaded() {
  if (LiveLike._config.ready) {
    livelikeLoadedCallback();
  } else {
    setTimeout(hasLiveLikeLoaded, 500);
  }
}
hasLiveLikeLoaded();
```

**Note:** The `LiveLike.init` method returns a Promise which resolves the LiveLike profile. Once this profile is resolved, you can be sure the SDK has loaded properly. If for some reason you can't implement this Promise resolution, you can also use the `LiveLike._config.ready` boolean property to ensure the SDK has loaded.

## Profile

### Getting Profile

```js
LiveLike.getUserProfile({
  accessToken: "<your-access-token>",
}).then((profile) => console.log(profile));
```

### Updating Profile

```js
LiveLike.updateUserProfile({
  accessToken: "<your-access-token>",
  options: {
    nickname: "<your-nickname>",
    custom_data: JSON.stringify({ customProp: "<your-custom-data>" }),
  },
}).then((updatedProfile) => console.log(updatedProfile));
```

**Notes:** Both the `nickname` and `custom_data` properties are optional.

## Widgets

### Creating a custom pop-up mode

```html
<livelike-widgets programid="program-id" mode="customPopup"></livelike-widgets>

<script>
  const widgetContainer = document.querySelector("livelike-widgets");

  LiveLike.registerWidgetMode("customPopup", ({ widget }) =>
    widgetContainer
      .attach(widget)
      .then(widget.interactive)
      .then(widget.results)
      .then(widget.expire)
      .then(() => widgetContainer.detach(widget))
  );
</script>
```

### Creating a custom mode where widgets are interactive indefinitely

```html
<livelike-widgets
  programid="<your-program-id>"
  mode="foreverInteractive"
></livelike-widgets>

<script>
  const widgetContainer = document.querySelector("livelike-widgets");

  LiveLike.registerWidgetMode("foreverInteractive", ({ widget }) =>
    widgetContainer
      .attach(widget)
      .then(() => widget.interactive({ timeout: null }))
  );
</script>
```

### Creating a custom timeline mode

```html
<livelike-widgets
  programid="<your-program-id>"
  mode="customTimeline"
></livelike-widgets>

<script>
  const widgetContainer = document.querySelector("livelike-widgets");

  LiveLike.registerWidgetMode("customTimeline", ({ widget }) =>
    widgetContainer
      .attach(widget)
      .then(() =>
        widget.initialLoad
          ? widget.results()
          : widget.interactive().then(widget.results)
      )
  );

  LiveLike.getWidgets({ programId: "your-program-id" }).then((widgets) =>
    widgets.forEach((widgetPayload) => {
      widget.initialLoad = true;
      widgetContainer.showWidget({ widgetPayload });
    })
  );
</script>
```

### Creating a custom widget mode with animations

```html
<livelike-widgets
  programid="<your-program-id>"
  mode="customPopup"
></livelike-widgets>

<script>
  const widgetContainer = document.querySelector("livelike-widgets");

  LiveLike.registerWidgetMode("customPopup", ({ widget }) =>
    widgetContainer
      .attach(widget)
      .then(widget.interactive)
      .then(widget.results)
      .then(() => {
        function createAnimation() {
          return new Promise((resolve) => {
            const animationContainer = document.createElement("div");
            animationContainer.innerHTML = `
              <img src="../assets/animation.gif">
              <div>Thanks for playing!</div>
            `;
            widget.append(animationContainer);
            setTimeout(() => {
              animationContainer.remove();
              resolve();
            }, 6000);
          });
        }
        return createAnimation();
      })
      .then(() => widgetContainer.detach(widget))
  );
</script>
```

### Set widget theme styles

```js
LiveLike.applyTheme({
  widgets: {
    poll: {
      header: {
        background: { format: "fill", color: "#0000ff" },
      },
      selectedOptionDescription: {
        fontColor: "#000000",
      },
    },
    quiz: {
      header: {
        background: { format: "fill", color: "#ff0000" },
      },
    },
  },
});
```

### Set widget translations

```js
LiveLike.applyLocalization({
  clientId: "<your-client-id>",
  localizedStrings: {
    en: {
      "widget.quiz.voteButton.label": "Vote now",
    },
    es: {
      "widget.quiz.voteButton.label": "Vota ahora",
    },
  },
});
```

### Add sounds to widget interactions

```js
const widgetContainer = document.querySelector("livelike-widgets");

widgetContainer.addEventListener("interacted", (e) => {
  const widgetAudio = new Audio("./sounds/cheer.mp3");
  widgetAudio.play();
});
```

**Note:** When the widget option is selected, audio is played.

### Displaying a single widget HTML tag

```html
<livelike-text-poll widgetid="<widget-id>"></livelike-text-poll>
```

**Note:** This widget has already been published and exists on the server. The `widgetid` attribute is the `id` of the widget in the widget's resource in the backend.

### Displaying a preview widget

```js
const textPoll = document.createElement("text-poll");
textPoll.kind = "text-poll";
textPoll.widgetPayload = { id: "" };
textPoll.question = "Example Poll Question";
textPoll.options = [
  { description: "Option One" },
  { description: "Option Two" },
];
document.body.append(textPoll);
```

**Note:** This is a widget that has not been published, and does not exist on the server. It is a static widget to display the UI.

### Creating widget element programmatically

```js
const widgetContainer = document.querySelector("livelike-widgets");

LiveLike.init({ clientId: "<your-client-id>" }).then(() => {
  widgetContainer.createWidgetElement({
    kind: "<widget-kind>",
    id: "<widget-id>",
  });
});
```

### Creating widget element programmatically with custom mode

```js
const widgetContainer = document.querySelector("livelike-widgets");

LiveLike.init({ clientId: "<your-client-id>" }).then(() => {
  widgetContainer.createWidgetElement({
    kind: "<widget-kind>",
    id: "<widget-id>",
    mode: ({ widget }) => widgetContainer.attach(widget).then(widget.results),
  });
});
```

### Creating custom widget template

```html
<style>
  .custom-widget livelike-widget-header {
    background: #232d37;
  }
  .custom-widget livelike-timer {
    background: #fac83c;
    height: 5px;
  }
  .custom-widget livelike-title {
    color: #fff;
    font-size: 1.25rem;
  }
  .custom-widget livelike-widget-body {
    background: #232d37;
    padding: 1.5rem;
  }
</style>
<template kind="text-poll">
  <livelike-widget-root class="custom-widget">
    <livelike-widget-header slot="header">
      <livelike-timer></livelike-timer>
      <livelike-title></livelike-title>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select>
        <template>
          <livelike-option>
            <div style="width:100%;display:flex;align-items:center;">
              <livelike-progress></livelike-progress>
              <livelike-description></livelike-description>
              <livelike-percentage></livelike-percentage>
            </div>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```