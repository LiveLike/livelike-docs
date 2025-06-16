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
[block:api-header]
{
  "title": "Getting started"
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Minimum supported engagement SDK",
  "body": "Web engagement SDK version: 2.24.0"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "API documentation",
  "body": "Refer [sceenic-plugin API documentation](https://websdk.livelikecdn.com/sceenic-plugin-docs/) for more details"
}
[/block]

[block:api-header]
{
  "title": "Install the sceenic plugin:"
}
[/block]
Install sceenic plugin from npm registry. Sceenic plugin is published in 3 variants:
1. ES module (livelike-sceenic-plugin.min.js)
2. Common JS (livelike-sceenic-plugin.cjs.js)
3. UMD (livelike-sceenic-plugin.umd.js)

When installed using npm, the ES module variant is been used. To use umd bundle refer below html snippet
[block:code]
{
  "codes": [
    {
      "code": "npm install @livelike/sceenic-plugin",
      "language": "javascript",
      "name": "ES Module"
    },
    {
      "code": "<script src=\"https://unpkg.com/@livelike/sceenic-plugin/livelike-sceenic-plugin.umd.js\"></script>",
      "language": "html",
      "name": "HTML"
    }
  ]
}
[/block]
To install a specific version of sceenic-plugin

```bash
npm install @livelike/sceenic-plugin@0.0.1-alpha.6
```
[block:api-header]
{
  "title": "Initialise the sceenic plugin:"
}
[/block]
Initialise the sceenic plugin passing the livelike API provider
[block:callout]
{
  "type": "warning",
  "title": "Initialise web engagement sdk",
  "body": "Make sure to initialise web engagement sdk with the procured client id, refer [web sdk getting started](getting-started-with-the-web-sdk) for more details"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Code snippet variations",
  "body": "ES Module: code snippet when integrating using ES module\nHTML UMD: code snippet when integrating using UMD sceenic-plugin bundle"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "import LiveLike from '@livelike/engagementsdk';\nimport { init } from '@livelike/sceenic-plugin';\n\ninit({\n    liveLikeApiProvider: LiveLike\n}).then((pluginInstance) => {\n// post sceenic plugin initialisation logic\n});\n\n// Also initialise livelike web sdk\nLiveLike.init({\n\tclientId: \"<your clientId>\"\n}).then((userprofile) => {\n// post web engagement sdk initialisation logic\n});",
      "language": "javascript",
      "name": "ES Module"
    },
    {
      "code": "<script>\n// make sure to include livelike umd script as well which would \n// expose `LiveLike` reference on window object\nLiveLikeSceenicPlugin.init({\n    liveLikeApiProvider: window.LiveLike\n}).then((pluginInstance) => {\n// post sceenic plugin initialisation logic\n});\n\nwindow.LiveLike.init({\n\tclientId: \"<your clientId>\"\n}).then((userprofile) => {\n// post initialisation logic\n})\n</script>",
      "language": "html",
      "name": "HTML UMD"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Render `sceenic-video-room`:"
}
[/block]
`sceenic-video-room` is a web component which could be used for a seamless integration which gives pre-baked functionality of:

* creating a video room
* joining a video room
* rendering participant videos
* leaving a video room
* mute/unmute local participant audio
* show/hide local participant video
[block:code]
{
  "codes": [
    {
      "code": "<body>\n\t<sceenic-video-room></sceenic-video-room>\n</body>",
      "language": "html"
    }
  ]
}
[/block]
#### `sceenic-video-room`  web component properties:
[block:parameters]
{
  "data": {
    "h-0": "Property name",
    "h-1": "Description",
    "0-0": "aspectratio",
    "0-1": "Set aspect ratio of the participant video (default is 4/3)",
    "1-0": "minvideowidth",
    "1-1": "Set minimum video width of each participant (default is auto calculated based on parent container of sceenic-video-room)",
    "2-0": "minvideoheight",
    "2-1": "Set minimum video height of each participant (default is auto calculated based on parent container of sceenic-video-room)"
  },
  "cols": 2,
  "rows": 3
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "<body>\n<sceenic-video-room\n    aspectratio=1.7778\n    minvideowidth=150\n    minvideoheight=84 \n>\n</sceenic-video-room>\n</body>",
      "language": "html"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Customise `sceenic-video-room`:"
}
[/block]
When there is a need to customise `sceenic-video-room` stock UI, extend `SceenicVideoRoom` Web component class and custom render parts of stock UI based on your level of customisation.

**For example, customising session entry controls**
[block:code]
{
  "codes": [
    {
      "code": "// use html API from sceenic-plugin to create lit template \n// https://lit.dev/docs/v1/lit-html/writing-templates/\nimport { SceenicVideoRoom, html } from '@livelike/sceenic-plugin\";\n\nclass CustomSceenicVideoRoom extends SceenicVideoRoom {\n    renderSessionEntryControls() {\n        return html`\n          <div>\n          <div class=\"session-entry\">\n              <button\n                id=\"create-call-control\"\n                class=\"control-button my-test\"\n                title=\"Create Video Room\"\n                @click=${this.createVideoRoom}\n                style=\"color: white;\"\n              >\n                Create\n              </button>\n              <div class=\"join-control\">\n                <input id=\"video-room-id\" type=\"text\" placeholder=\"Video Room Id\" />\n                <button\n                  class=\"control-button join-control-button\"\n                  title=\"Join Video Room\"\n                  @click=${this.joinVideoRoom}\n                  style=\"color: white;\"\n                >\n                    Join\n                </button>\n              </div>\n            </div>\n            <p style=\"color: red;\">Sponsored by: Livelike</p>\n            </div>\n          `;\n    }\n}\n\nif (!customElements.get(\"custom-sceenic-video-room\")) {\n  customElements.define(\"custom-sceenic-video-room\", CustomSceenicVideoRoom);\n}",
      "language": "javascript"
    },
    {
      "code": "<script>\nclass CustomSceenicVideoRoom extends LiveLikeSceenicPlugin.SceenicVideoRoom {\n    renderSessionEntryControls() {\n        return LiveLikeSceenicPlugin.html`\n          <div>\n          <div class=\"session-entry\">\n              <button\n                id=\"create-call-control\"\n                class=\"control-button my-test\"\n                title=\"Create Video Room\"\n                @click=${this.createVideoRoom}\n                style=\"color: white;\"\n              >\n                Create\n              </button>\n              <div class=\"join-control\">\n                <input id=\"video-room-id\" type=\"text\" placeholder=\"Video Room Id\" />\n                <button\n                  class=\"control-button join-control-button\"\n                  title=\"Join Video Room\"\n                  @click=${this.joinVideoRoom}\n                  style=\"color: white;\"\n                >\n                    Join\n                </button>\n              </div>\n            </div>\n            <p style=\"color: red;\">Sponsored by: Livelike</p>\n            </div>\n          `;\n    }\n}\n\n  if (!customElements.get(\"custom-sceenic-video-room\")) {\n    customElements.define(\"custom-sceenic-video-room\", CustomSceenicVideoRoom);\n  }\n</script>",
      "language": "html",
      "name": "HTML UMD"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Implement Custom UI:"
}
[/block]
In case, you want to integrate sceenic-plugin in UI frameworks like React, Angular, Vue.js etc. this would require you to implement custom UI based on framework API's.
This could be achieved with the use of plugin instance - `service`, `model` and `serviceProvider`.
[block:api-header]
{
  "title": "What is Plugin instance?"
}
[/block]
Plugin instance is an object which could be used to implement video room features in any JS framework with the following properties:

```js
const { service, model, serviceProvider } = pluginInstance;
``` 

#### 1. `service` - reference to plugin service which contains actions API to create, join and manage a video room session. 
    1. createVideoRoom() - To create and join a new video room session 
    2. joinVideoRoom(videoRoomId) - To join an existing video room using a given video id
    3. enableAudio(status): Enable/Disable mic audio
    4. enableVideo(status): Enable/Disable local user video
    5. leaveVideoRoom() - Leave the joined video room
    6. addVideoRoomEventListener(VideoRoomEvent, listenerFn): Add custom use cases in the form of listener fn which gets invoked based on given sceenic event.
    7. removeVideoRoomEventListener(VideoRoomEvent, listenerFn): remove attached listener function

#### 2. `serviceProvider` - reference of underlying service provider, incase you want to directly use third part service client for your custom use cases.
Refer [sceenic documentation](https://documentation.sceenic.co/watch-together-sdk/sscale-confluence-api-references/sscale-confluence-web-sdk-reference) for more details on sceenic serviceProvider.

#### 3. `model` - reference to service model instance (similar to reactive UI state) which maintains a video room session data:
    1. getData() - returns the current model data
    2. setData(modelData) - to set the model data which internally publishes to all the model subscribers
    3. subscribe(subscriberFn) - subscribe to the reactive model data where the subscriber function is called whenever model data gets changed.


#### Model data object properties:

[block:parameters]
{
  "data": {
    "h-0": "Property Name",
    "h-1": "Property Description",
    "0-0": "audioEnabled",
    "0-1": "flag to check whether local user audio is enabled or disabled. (type boolean, default true)",
    "1-0": "videoEnabled",
    "1-1": "flag to check whether local user video is enabled or disabled. (type boolean, default true)",
    "2-0": "participants",
    "2-1": "Array of participants videos (type [ISceenicParticipant](https://websdk.livelikecdn.com/sceenic-plugin-docs/0.0.1-alpha.0/interfaces/_internal_.ISceenicParticipant.html), default empty array)",
    "3-0": "videoRoomId",
    "4-0": "connectionStatus",
    "4-1": "Video room connection state of value - `\"CONNECTED\"` | `\"DISCONNECTED\"`.\nInitially it is `\"DISCONNECTED\"` until user creates or joins a video room post which connectionStatus changes to `\"CONNECTED\"`.",
    "3-1": "video room identifier which could be used by other user to join an existing video room(type string, default undefined)"
  },
  "cols": 2,
  "rows": 5
}
[/block]

[block:api-header]
{
  "title": "How to get plugin instance?"
}
[/block]
There's two ways to get plugin instance:

#### 1.  Initialising sceenic-plugin returns a promise whose resolved value is a plugin instance.
[block:code]
{
  "codes": [
    {
      "code": "import { init } from '@livelike/sceenic-plugin';\n \ninit({\n    liveLikeApiProvider: window.LiveLike\n}).then(pluginInstance => {\n\tconst { service, model, serviceProvider } = pluginInstance; \n})",
      "language": "javascript",
      "name": "ES Module"
    },
    {
      "code": "<script>\nLiveLikeSceenicPlugin.init({\n    liveLikeApiProvider: window.LiveLike\n}).then(pluginInstance => {\n   const {service, model, serviceProvider} = pluginInstance\n});\n</script>",
      "language": "html",
      "name": "HTML UMD"
    }
  ]
}
[/block]
#### 2. addPluginEventListener:
listener for event `PluginEvent.PLUGIN_INITIALISED` get called with plugin instance. This could be used incase your init work flow is different then the UI component for eg:  init is done during script loading which lazily loads application UI component where maintaining and passing plugin instance to lazily loaded UI component could result in unnecessary complexity.
[block:code]
{
  "codes": [
    {
      "code": "import { addPluginEventListener, PluginEvent } from '@livelike/sceenic-plugin';\n\nfunction onPluginInitialised(pluginInstance){\n    const {service, model, serviceProvider} = pluginInstance\n    //use service actions like create, join, leave or subsscribe to model\n}\n\naddPluginEventListener(\n    PluginEvent.PLUGIN_INITIALISED,\n    onPluginInitialised\n)",
      "language": "javascript",
      "name": "ES Module"
    },
    {
      "code": "<script>\n  function onPluginInitialised(pluginInstance){\n    const {service, model, serviceProvider} = pluginInstance\n    //use service actions like create, join, leave or subsscribe to model\n}\n\nLiveLikeSceenicPlugin.addPluginEventListener(\n    LiveLikeSceenicPlugin.PluginEvent.PLUGIN_INITIALISED,\n    onPluginInitialised\n)\n</script>",
      "language": "html",
      "name": "HTML UMD"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "React.js sample code for Custom UI",
  "body": "Refer custom UI implementation for [React.js framework](https://stackblitz.com/edit/vitejs-vite-cmtppp?file=src/App.jsx) using plugin instance.\n**Note: Update web engagement sdk initialisation with procured clientId in code sample**"
}
[/block]

[block:api-header]
{
  "title": "Video call feature implementation in native JS"
}
[/block]
### Render Participant videos:
Subscribe to model data using `pluginInstance.model.subscribe` which would give you list of participant video.
[block:code]
{
  "codes": [
    {
      "code": "function renderParticipantVideo({ local, stream, participantId }){\n    const node = document.getElementById(participantId);\n\n    if(node) {\n        node.srcObject = stream;\n    } else {\n        const div = document.createElement(\"div\")\n        div.setAttribute(\"class\", \"video-container\");\n\n        const video = document.createElement(\"video\");\n        video.id = participantId;\n        video.className = local ? \"local\" : \"\";\n        video.autoplay = true;\n        video.muted = local;\n        video.srcObject = stream;\n        video.playsInline = true;\n        video.disablePictureInPicture = true;\n\n        div.appendChild(video)\n\n        const container = document.querySelector(\"#gallery\");\n        container.appendChild(div);\n    }\n}\n\nfunction removeParticipantVideos(participants){\n   const participantIds = participants.map(({participantId}) => participantId);\n   const videoElements = Array.from(document.querySelectorAll('#gallery video'));\n   videoElements\n   .filter(videoEl => !participantIds.includes(videoEl.id))\n   .map(videoEl => {\n        videoEl.parentElement.remove();\n   })\n}\n\nfunction modelsubscriber(modelData){\n    const {participants} = modelData;\n    // remove older participants videos\n    removeParticipantVideos(participants);\n    // render current participants videos\n    participants.map(renderParticipantVideo)\n}\n\n// using reference of pluginInstance\nconst unsubscribe = pluginInstance.model.subscribe(modelsubscriber);\n// unsubscribe when UI unmounts",
      "language": "javascript"
    }
  ]
}
[/block]
### Create a video room:
To create a video room, get the plugin instance service reference and call `createVideoRoom` method.
**Below snippet assumes button with id `create-button-id` already present in html.**
[block:code]
{
  "codes": [
    {
      "code": "const createButton = document.querySelector('#create-button-id')\n\ncreateButton.addEventListener('click', function (){\n   // using reference of pluginInstance\n    pluginInstance.service.createVideoRoom();\n})\n\n// Render participant videos (refer \"Render Participant videos\" docs)",
      "language": "javascript"
    }
  ]
}
[/block]
### Join a video room:
For joining a video room, one needs a video room id. Get the plugin instance service reference and call `joinVideoRoom` method which takes a video room ID and an optional participant Name as string.
**Below snippet assumes button with id `join-button-id` already present in html.**
[block:code]
{
  "codes": [
    {
      "code": "const joinButton = document.querySelector('#join-button-id')\n\njoinButton.addEventListener('click', function (){\n    // using reference of pluginInstance\n    pluginInstance.service.joinVideoRoom('ca62dae2-3901-40d5-bc2d-ad53a223689e');\n})\n\n// Render participant videos (refer \"Render Participant videos\" docs)",
      "language": "javascript"
    }
  ]
}
[/block]
### Leave a video room:
To leave a video room, get the plugin instance service reference and call `leaveVideoRoom` method which lets participant leave the currently joined video room.
**Below snippet assumes button with id `leave-button-id` already present in html.**
[block:code]
{
  "codes": [
    {
      "code": "const leaveButton = document.querySelector('#leave-button-id')\n\nleaveButton.addEventListener('click', function (){\n    // using reference of pluginInstance\n    pluginInstance.service.leaveVideoRoom();\n})\n\n// Render participant videos (refer \"Render Participant videos\" docs)",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Video Room Event:"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Override sceenic callbacks",
  "body": "To override complete behaviour of participant add and participant left logic, refer [Sceenic docs] (https://documentation.sceenic.co/watch-together-sdk/sscale-confluence-api-references/sscale-confluence-web-sdk-reference/sscale-confluence-participantlisteners-websdk)"
}
[/block]
In case there’s any custom UI requirement for eg: adding a banner whenever user join/leave a video room, you could attach an event listener and add your own custom logic.

### `VideoRoomEvent.PARTICIPANT_JOIN` 
Attach a listener to add custom logic whenever a participant joins a video call
[block:code]
{
  "codes": [
    {
      "code": "function onParticipantJoin(participant){\n   // custom logic\n}\n// using reference of pluginInstance\npluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_JOIN, onParticipantJoin)\n\n// To remove the attached listener\npluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_JOIN, onParticipantJoin)",
      "language": "javascript"
    }
  ]
}
[/block]
### `VideoRoomEvent.PARTICIPANT_LEFT` 
Attach a listener to add custom logic whenever a participant leaves a video call
[block:code]
{
  "codes": [
    {
      "code": "function onParticipantLeft(participant){\n   // custom logic\n}\n// using reference of pluginInstance\npluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_LEFT, onParticipantLeft)\n\n// To remove the attached listener\npluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.PARTICIPANT_LEFT, onParticipantLeft)",
      "language": "javascript"
    }
  ]
}
[/block]
### `VideoRoomEvent.ERROR`
Attach a listener to add custom logic whenever a video room or video session related error occurs for eg: error when network disconnected, max participant limit reached, expired video session, etc.
[block:code]
{
  "codes": [
    {
      "code": "function onError(errorDetails){\n   // custom logic\n}\n// using reference of pluginInstance\npluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.ERROR, onError)\n\n// To remove the attached listener\npluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.ERROR, onError)",
      "language": "javascript"
    }
  ]
}
[/block]
### `VideoRoomEvent.RECONNECTING`
Attach a listener to add custom logic whenever a user video session is reconnecting for eg: showing a reconnecting banner or showing alternate UI while reconnecting. You can subscribe to service model data which would give you the latest state of `connectionStatus`.
[block:code]
{
  "codes": [
    {
      "code": "function onReconnecting(){\n   // custom logic\n}\n// using reference of pluginInstance\npluginInstance.service.addVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.RECONNECTING, onReconnecting)\n\n// To remove the attached listener\npluginInstance.service.removeVideoRoomEventListener(LiveLikeSceenicPlugin.VideoRoomEvent.RECONNECTING, onReconnecting)",
      "language": "javascript"
    }
  ]
}
[/block]