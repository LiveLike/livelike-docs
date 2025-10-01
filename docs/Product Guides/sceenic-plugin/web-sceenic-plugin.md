---
title: Sceenic Plugin for Web
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
## Getting started

> 🚧 Minimum supported engagement SDK
>
> Web engagement SDK version: 2.24.0

> 📘 API documentation
>
> Refer [sceenic-plugin API documentation](https://websdk.livelikecdn.com/sceenic-plugin-docs/) for more details

## Install the sceenic plugin:

Install sceenic plugin from npm registry. Sceenic plugin is published in 3 variants:

1. ES module (livelike-sceenic-plugin.min.js)
2. Common JS (livelike-sceenic-plugin.cjs.js)
3. UMD (livelike-sceenic-plugin.umd.js)

When installed using npm, the ES module variant is been used. To use umd bundle refer below html snippet

```javascript ES Module
npm install @livelike/sceenic-plugin
```
```html HTML
<script src="https://unpkg.com/@livelike/sceenic-plugin/livelike-sceenic-plugin.umd.js"></script>
```

To install a specific version of sceenic-plugin

```bash
npm install @livelike/sceenic-plugin@0.0.1-alpha.6
```

## Initialise the sceenic plugin:

Initialise the sceenic plugin passing the livelike API provider

> 🚧 Initialise web engagement sdk
>
> Make sure to initialise web engagement sdk with the procured client id, refer [web sdk getting started](getting-started-with-the-web-sdk) for more details

> 📘 Code snippet variations
>
> ES Module: code snippet when integrating using ES module\
> HTML UMD: code snippet when integrating using UMD sceenic-plugin bundle

```javascript ES Module
import LiveLike from '@livelike/engagementsdk';
import { init } from '@livelike/sceenic-plugin';

init({
    liveLikeApiProvider: LiveLike
}).then((pluginInstance) => {
// post sceenic plugin initialisation logic
});

// Also initialise livelike web sdk
LiveLike.init({
	clientId: "<your clientId>"
}).then((userprofile) => {
// post web engagement sdk initialisation logic
});
```
```html HTML UMD
<script>
// make sure to include livelike umd script as well which would 
// expose `LiveLike` reference on window object
LiveLikeSceenicPlugin.init({
    liveLikeApiProvider: window.LiveLike
}).then((pluginInstance) => {
// post sceenic plugin initialisation logic
});

window.LiveLike.init({
	clientId: "<your clientId>"
}).then((userprofile) => {
// post initialisation logic
})
</script>
```

## Render `sceenic-video-room`:

`sceenic-video-room` is a web component which could be used for a seamless integration which gives pre-baked functionality of:

* creating a video room
* joining a video room
* rendering participant videos
* leaving a video room
* mute/unmute local participant audio
* show/hide local participant video

```html
<body>
	<sceenic-video-room></sceenic-video-room>
</body>
```

#### `sceenic-video-room`  web component properties:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property name
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        aspectratio
      </td>

      <td>
        Set aspect ratio of the participant video (default is 4/3)
      </td>
    </tr>

    <tr>
      <td>
        minvideowidth
      </td>

      <td>
        Set minimum video width of each participant (default is auto calculated based on parent container of sceenic-video-room)
      </td>
    </tr>

    <tr>
      <td>
        minvideoheight
      </td>

      <td>
        Set minimum video height of each participant (default is auto calculated based on parent container of sceenic-video-room)
      </td>
    </tr>
  </tbody>
</Table>

```html
<body>
<sceenic-video-room
    aspectratio=1.7778
    minvideowidth=150
    minvideoheight=84 
>
</sceenic-video-room>
</body>
```

## Customise `sceenic-video-room`:

When there is a need to customise `sceenic-video-room` stock UI, extend `SceenicVideoRoom` Web component class and custom render parts of stock UI based on your level of customisation.

**For example, customising session entry controls**

```javascript
// use html API from sceenic-plugin to create lit template 
// https://lit.dev/docs/v1/lit-html/writing-templates/
import { SceenicVideoRoom, html } from '@livelike/sceenic-plugin";

class CustomSceenicVideoRoom extends SceenicVideoRoom {
    renderSessionEntryControls() {
        return html`
          <div>
          <div class="session-entry">
              <button
                id="create-call-control"
                class="control-button my-test"
                title="Create Video Room"
                @click=${this.createVideoRoom}
                style="color: white;"
              >
                Create
              </button>
              <div class="join-control">
                <input id="video-room-id" type="text" placeholder="Video Room Id" />
                <button
                  class="control-button join-control-button"
                  title="Join Video Room"
                  @click=${this.joinVideoRoom}
                  style="color: white;"
                >
                    Join
                </button>
              </div>
            </div>
            <p style="color: red;">Sponsored by: Livelike</p>
            </div>
          `;
    }
}

if (!customElements.get("custom-sceenic-video-room")) {
  customElements.define("custom-sceenic-video-room", CustomSceenicVideoRoom);
}
```
```html HTML UMD
<script>
class CustomSceenicVideoRoom extends LiveLikeSceenicPlugin.SceenicVideoRoom {
    renderSessionEntryControls() {
        return LiveLikeSceenicPlugin.html`
          <div>
          <div class="session-entry">
              <button
                id="create-call-control"
                class="control-button my-test"
                title="Create Video Room"
                @click=${this.createVideoRoom}
                style="color: white;"
              >
                Create
              </button>
              <div class="join-control">
                <input id="video-room-id" type="text" placeholder="Video Room Id" />
                <button
                  class="control-button join-control-button"
                  title="Join Video Room"
                  @click=${this.joinVideoRoom}
                  style="color: white;"
                >
                    Join
                </button>
              </div>
            </div>
            <p style="color: red;">Sponsored by: Livelike</p>
            </div>
          `;
    }
}

  if (!customElements.get("custom-sceenic-video-room")) {
    customElements.define("custom-sceenic-video-room", CustomSceenicVideoRoom);
  }
</script>
```

## Implement Custom UI:

In case, you want to integrate sceenic-plugin in UI frameworks like React, Angular, Vue.js etc. this would require you to implement custom UI based on framework API's.\
This could be achieved with the use of plugin instance - `service`, `model` and `serviceProvider`.

## What is Plugin instance?

Plugin instance is an object which could be used to implement video room features in any JS framework with the following properties:

```js
const { service, model, serviceProvider } = pluginInstance;
```

#### 1. `service` - reference to plugin service which contains actions API to create, join and manage a video room session.

```
1. createVideoRoom() - To create and join a new video room session 
2. joinVideoRoom(videoRoomId) - To join an existing video room using a given video id
3. enableAudio(status): Enable/Disable mic audio
4. enableVideo(status): Enable/Disable local user video
5. leaveVideoRoom() - Leave the joined video room
6. addVideoRoomEventListener(VideoRoomEvent, listenerFn): Add custom use cases in the form of listener fn which gets invoked based on given sceenic event.
7. removeVideoRoomEventListener(VideoRoomEvent, listenerFn): remove attached listener function
```

#### 2. `serviceProvider` - reference of underlying service provider, incase you want to directly use third part service client for your custom use cases.

Refer [sceenic documentation](https://documentation.sceenic.co/watch-together-sdk/sscale-confluence-api-references/sscale-confluence-web-sdk-reference) for more details on sceenic serviceProvider.

#### 3. `model` - reference to service model instance (similar to reactive UI state) which maintains a video room session data:

```
1. getData() - returns the current model data
2. setData(modelData) - to set the model data which internally publishes to all the model subscribers
3. subscribe(subscriberFn) - subscribe to the reactive model data where the subscriber function is called whenever model data gets changed.
```

#### Model data object properties:

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Property Name
      </th>

      <th>
        Property Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        audioEnabled
      </td>

      <td>
        flag to check whether local user audio is enabled or disabled. (type boolean, default true)
      </td>
    </tr>

    <tr>
      <td>
        videoEnabled
      </td>

      <td>
        flag to check whether local user video is enabled or disabled. (type boolean, default true)
      </td>
    </tr>

    <tr>
      <td>
        participants
      </td>

      <td>
        Array of participants videos (type [ISceenicParticipant](https://websdk.livelikecdn.com/sceenic-plugin-docs/0.0.1-alpha.0/interfaces/_internal_.ISceenicParticipant.html), default empty array)
      </td>
    </tr>

    <tr>
      <td>
        videoRoomId
      </td>

      <td>
        video room identifier which could be used by other user to join an existing video room(type string, default undefined)
      </td>
    </tr>

    <tr>
      <td>
        connectionStatus
      </td>

      <td>
        Video room connection state of value - `"CONNECTED"` | `"DISCONNECTED"`.\
        Initially it is `"DISCONNECTED"` until user creates or joins a video room post which connectionStatus changes to `"CONNECTED"`.
      </td>
    </tr>
  </tbody>
</Table>

## How to get plugin instance?

There's two ways to get plugin instance:

#### 1.  Initialising sceenic-plugin returns a promise whose resolved value is a plugin instance.

```javascript ES Module
import { init } from '@livelike/sceenic-plugin';
 
init({
    liveLikeApiProvider: window.LiveLike
}).then(pluginInstance => {
	const { service, model, serviceProvider } = pluginInstance; 
})
```
```html HTML UMD
<script>
LiveLikeSceenicPlugin.init({
    liveLikeApiProvider: window.LiveLike
}).then(pluginInstance => {
   const {service, model, serviceProvider} = pluginInstance
});
</script>
```

#### 2. addPluginEventListener:

listener for event `PluginEvent.PLUGIN_INITIALISED` get called with plugin instance. This could be used incase your init work flow is different then the UI component for eg:  init is done during script loading which lazily loads application UI component where maintaining and passing plugin instance to lazily loaded UI component could result in unnecessary complexity.

```javascript ES Module
import { addPluginEventListener, PluginEvent } from '@livelike/sceenic-plugin';

function onPluginInitialised(pluginInstance){
    const {service, model, serviceProvider} = pluginInstance
    //use service actions like create, join, leave or subsscribe to model
}

addPluginEventListener(
    PluginEvent.PLUGIN_INITIALISED,
    onPluginInitialised
)
```
```html HTML UMD
<script>
  function onPluginInitialised(pluginInstance){
    const {service, model, serviceProvider} = pluginInstance
    //use service actions like create, join, leave or subsscribe to model
}

LiveLikeSceenicPlugin.addPluginEventListener(
    LiveLikeSceenicPlugin.PluginEvent.PLUGIN_INITIALISED,
    onPluginInitialised
)
</script>
```

> 📘 React.js sample code for Custom UI
>
> Refer custom UI implementation for [React.js framework](https://stackblitz.com/edit/vitejs-vite-cmtppp?file=src/App.jsx) using plugin instance.\
> **Note: Update web engagement sdk initialisation with procured clientId in code sample**

## Video call feature implementation in native JS

### Render Participant videos:

Subscribe to model data using `pluginInstance.model.subscribe` which would give you list of participant video.

```javascript
function renderParticipantVideo({ local, stream, participantId }){
    const node = document.getElementById(participantId);

    if(node) {
        node.srcObject = stream;
    } else {
        const div = document.createElement("div")
        div.setAttribute("class", "video-container");

        const video = document.createElement("video");
        video.id = participantId;
        video.className = local ? "local" : "";
        video.autoplay = true;
        video.muted = local;
        video.srcObject = stream;
        video.playsInline = true;
        video.disablePictureInPicture = true;

        div.appendChild(video)

        const container = document.querySelector("#gallery");
        container.appendChild(div);
    }
}

function removeParticipantVideos(participants){
   const participantIds = participants.map(({participantId}) => participantId);
   const videoElements = Array.from(document.querySelectorAll('#gallery video'));
   videoElements
   .filter(videoEl => !participantIds.includes(videoEl.id))
   .map(videoEl => {
        videoEl.parentElement.remove();
   })
}

function modelsubscriber(modelData){
    const {participants} = modelData;
    // remove older participants videos
    removeParticipantVideos(participants);
    // render current participants videos
    participants.map(renderParticipantVideo)
}

// using reference of pluginInstance
const unsubscribe = pluginInstance.model.subscribe(modelsubscriber);
// unsubscribe when UI unmounts
```

### Create a video room:

To create a video room, get the plugin instance service reference and call `createVideoRoom` method.\
**Below snippet assumes button with id`create-button-id` already present in html.**

```javascript
const createButton = document.querySelector('#create-button-id')

createButton.addEventListener('click', function (){
   // using reference of pluginInstance
    pluginInstance.service.createVideoRoom();
})

// Render participant videos (refer "Render Participant videos" docs)
```

### Join a video room:

For joining a video room, one needs a video room id. Get the plugin instance service reference and call `joinVideoRoom` method which takes a video room ID and an optional participant Name as string.\
**Below snippet assumes button with id`join-button-id` already present in html.**

```javascript
const joinButton = document.querySelector('#join-button-id')

joinButton.addEventListener('click', function (){
    // using reference of pluginInstance
    pluginInstance.service.joinVideoRoom('ca62dae2-3901-40d5-bc2d-ad53a223689e');
})

// Render participant videos (refer "Render Participant videos" docs)
```

### Leave a video room:

To leave a video room, get the plugin instance service reference and call `leaveVideoRoom` method which lets participant leave the currently joined video room.\
**Below snippet assumes button with id`leave-button-id` already present in html.**

```javascript
const leaveButton = document.querySelector('#leave-button-id')

leaveButton.addEventListener('click', function (){
    // using reference of pluginInstance
    pluginInstance.service.leaveVideoRoom();
})

// Render participant videos (refer "Render Participant videos" docs)
```

## Video Room Event:

> 📘 Override sceenic callbacks
>
> To override complete behaviour of participant add and participant left logic, refer [Sceenic docs] ([https://documentation.sceenic.co/watch-together-sdk/sscale-confluence-api-references/sscale-confluence-web-sdk-reference/sscale-confluence-participantlisteners-websdk](https://documentation.sceenic.co/watch-together-sdk/sscale-confluence-api-references/sscale-confluence-web-sdk-reference/sscale-confluence-participantlisteners-websdk))

In case there’s any custom UI requirement for eg: adding a banner whenever user join/leave a video room, you could attach an event listener and add your own custom logic.

### `VideoRoomEvent.PARTICIPANT_JOIN`

Attach a listener to add custom logic whenever a participant joins a video call

```javascript
function onParticipantJoin(participant){
   // custom logic
}
// using reference of pluginInstance
pluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_JOIN, onParticipantJoin)

// To remove the attached listener
pluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_JOIN, onParticipantJoin)
```

### `VideoRoomEvent.PARTICIPANT_LEFT`

Attach a listener to add custom logic whenever a participant leaves a video call

```javascript
function onParticipantLeft(participant){
   // custom logic
}
// using reference of pluginInstance
pluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_LEFT, onParticipantLeft)

// To remove the attached listener
pluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_LEFT, onParticipantLeft)
```

### `VideoRoomEvent.ERROR`

Attach a listener to add custom logic whenever a video room or video session related error occurs for eg: error when network disconnected, max participant limit reached, expired video session, etc.

```javascript
function onError(errorDetails){
   // custom logic
}
// using reference of pluginInstance
pluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.ERROR, onError)

// To remove the attached listener
pluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.ERROR, onError)
```

### `VideoRoomEvent.RECONNECTING`

Attach a listener to add custom logic whenever a user video session is reconnecting for eg: showing a reconnecting banner or showing alternate UI while reconnecting. You can subscribe to service model data which would give you the latest state of `connectionStatus`.

```javascript
function onReconnecting(){
   // custom logic
}
// using reference of pluginInstance
pluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.RECONNECTING, onReconnecting)

// To remove the attached listener
pluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.RECONNECTING, onReconnecting)
```
