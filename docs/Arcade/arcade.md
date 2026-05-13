---
title: Technical Integration Guide
excerpt: >-
  This guide outlines the steps for integrating the Arcade Games onto your
  website using the LiveLike Web SDK and Arcade Javascript SDK.
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
      slug: minigames-cms-guide
      title: MiniGames CMS Guide
---
## Click [here](https://docs.livelike.com/docs/minigames-cms-guide) to check out CMS Guide for setting up games.

### Prerequisites:

1. LiveLike Web SDK: LiveLike Web SDK Documentation
2. Arcade Game JavaScript SDK
3. Game ID and Instance ID: Obtain these from the Arcade CMS for the specific game you want to integrate.

<br />

### Step 1: Integrate LiveLike Web SDK

1. Follow the instructions provided in the LiveLike Web SDK documentation ([Web SDK](https://docs.livelike.com/docs/getting-started-with-the-web-sdk)) to integrate the LiveLike Web SDK into your website.
2. This involves adding the LiveLike SDK script and initializing the SDK with your project credentials.

<br />

### Step 2: Add the Arcade Game JavaScript SDKs

* **Guess The Word**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/guess-the-word-2.9.0.js"></script>

```

* **Guess The Image**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/guess-the-image-1.3.1.js"></script>

```

* **Trivia**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/trivia-1.7.1.js"></script>

```

* **Pick Your Team**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/pick-your-team-1.15.1.js"></script>
```

* **Play Predictor**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/predictor-1.10.0.js"></script>

```

* **Guess What**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/guess-what-1.2.0.js"></script>

```

* **Spin The Wheel**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/spin-the-wheel-1.2.0.js"></script>

```

* **Skill Game**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/skill-game-0.1.3.js"></script>

```

* **Sweepstakes**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/sweepstakes-0.2.0.js"></script>

```

* **Scratch Card**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/scratch-card-0.2.0.js"></script>
```

<br />

### Step 3: Embed Game Component

* In the body section of your HTML page, add the appropriate game component tag and replace the placeholders with your actual values:

<br />

* #### **Guess The Word** ([Demo](https://stackblitz.com/edit/livelike-gtw-bzlbxnum?file=package.json))

```html
<ll-guess-the-word accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-guess-the-word>

```

* #### **Guess The Image** ([Demo](https://stackblitz.com/edit/vitejs-vite-7wiwh6jm?file=index.html))

```html
<ll-guess-the-image accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-guess-the-image>

```

* #### **Trivia**: ([Demo](https://stackblitz.com/edit/vitejs-vite-utaxefne?file=package.json))

```html
<ll-trivia accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-trivia>

```

<Callout icon="📘" theme="info">
  **Note:** `instanceId` is optional. If you don't pass it, `<ll-trivia>` will automatically pick the right trivia to show based on the current time and the schedule of available trivia instances for the given `gameId`.
</Callout>

* #### **Pick Your Team**: ([Demo](https://stackblitz.com/edit/vitejs-vite-nez9f9nx?file=package.json))

```html
<ll-pick-your-team accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-pick-your-team>
```

* #### **Play Predictor**: ([Demo](https://stackblitz.com/edit/vitejs-vite-bnf79vqn?file=package.json))

```html html
<ll-predictor accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-predictor>
```

* #### **Guess What**: ([Demo](https://stackblitz.com/edit/vitejs-vite-atjqhe2q?file=package.json))

```html html
<ll-guess-what accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-guess-what>
```

* #### **Spin The Wheel**: ([Demo](https://stackblitz.com/edit/vitejs-vite-lu5379v7?file=index.html))

```html html
<ll-spin-the-wheel accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-spin-the-wheel>
```

* #### **Skill Games**: ([Demo](https://stackblitz.com/edit/livelike-skill-game))

```html html
<ll-skill-game accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-skill-game>
```

* #### **Sweepstakes**

```html html
<ll-sweepstakes accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-sweepstakes>
```

* #### **Scratch Card**

```html html
<ll-scratch-card accessToken=${accessToken} profileId=${profileId} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-scratch-card>
```

<br />

### Required Parameters:

* **profileId** and **authToken**: These values are obtained through the LiveLike platform for user authentication.
* **gameId** and **instanceId**: These are unique identifiers for the specific game instance and can be retrieved from Arcade CMS.

## Please Note

* Games that require **social sharing or download image enablement** (_for games that supports it_) from native Android or iOS apps also need corresponding configuration on the app side. Please refer to the implementation guide here for detailed setup instructions. [here](https://docs.livelike.com/update/docs/native-share-and-download-interface-integration-ios-android-react-native#/)
