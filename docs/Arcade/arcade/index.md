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
<script type="module" src="https://arcade-web.livelikecdn.com/guess-the-word-2.3.1.js"></script>

```

* **Trivia**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/trivia-1.5.1.js"></script>

```

* **Pick Your Team**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/pick-your-team-1.1.0.js"></script>
```

* **Play Predictor**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/predictor-1.1.0.js"></script>

```

* **Guess What**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/guess-what-1.0.0.js"></script>

```

* **Spin The Wheel**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/spin-the-wheel-1.1.1.js"></script>

```

* **Skill Game**: Add the following script tag to your HTML page:

```html
<script type="module" src="https://arcade-web.livelikecdn.com/skill-game-0.1.2.js"></script>

```

<br />

### Step 3: Embed Game Component

* In the body section of your HTML page, add the appropriate game component tag and replace the placeholders with your actual values:

<br />

* #### **Guess The Word** ([Demo](https://stackblitz.com/edit/livelike-gtw))

```html
<ll-guess-the-word accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-guess-the-word>

```

* #### **Trivia**: ([Demo](https://stackblitz.com/edit/livelike-trivia))

```html
<ll-trivia profileId=${profileId} accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-trivia>

```

* #### **Pick Your Team**: ([Demo](https://stackblitz.com/edit/livelike-pyt))

```html
<ll-pick-your-team accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-pick-your-team>
```

* #### **Play Predictor**: ([Demo](https://stackblitz.com/edit/react-vxwfaksw?file=src%2FApp.js))

```html html
<ll-predictor accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-predictor>
```

* #### **Guess What**: ([Demo](https://stackblitz.com/edit/vitejs-vite-orguuifq))

```html html
<ll-guess-what accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-guess-what>
```

* #### **Spin The Wheel**: ([Demo](https://stackblitz.com/edit/vitejs-vite-nsxe4pgr?file=src%2FApp.jsx))

```html html
<ll-spin-the-wheel profileId=${profileId} accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-spin-the-wheel>
```

* #### **Skill Games**: ([Demo](https://stackblitz.com/edit/livelike-skill-game))

```html html
<ll-skill-game accessToken=${accessToken} clientId=${clientId} gameId=${gameId} instanceId=${instanceId}></ll-skill-game>
```

### Required Parameters:

* **profileId** and **authToken**: These values are obtained through the LiveLike platform for user authentication.
* **gameId** and **instanceId**: These are unique identifiers for the specific game instance and can be retrieved from Arcade CMS.

## Please Note 

* Games that require **social sharing or download image enablement** (_for games that supports it_) from native Android or iOS apps also need corresponding configuration on the app side. Please refer to the implementation guide here for detailed setup instructions. [here](https://docs.livelike.com/update/docs/native-share-and-download-interface-integration-ios-android-react-native#/)
