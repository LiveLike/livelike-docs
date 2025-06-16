---
title: Widget Modes
excerpt: Different ways of displaying and interacting with widgets
deprecated: false
hidden: false
metadata:
  title: Widget Modes | Web SDK | Interactive Tools | LiveLike
  description: >-
    The LiveLike widgets element has two built-in modes: the default popup mode
    and the timeline mode. Learn more about widget modes.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: live-blog-tutorial
      title: Live Blog Tutorial
---
The `livelike-widgets` element has two built-in modes: the default `pop-up` mode, and the `timeline` mode. In pop-up mode, widgets appear for a limited time and then disappear. In timeline mode, a list of previously published widgets is loaded immediately, and then new widgets appear and stack up on top of older ones.

## Popup Mode

Widgets appear for a limited time and then disappear. They are interactive until the timer animation runs out. It is typically used for live interactive experiences.

```html
<!-- The mode attribute is optional and defaults to popup -->
<livelike-widgets programid="example-program-id" mode="pop-up">
</livelike-widgets>
```

## Timeline Mode

Previously published widgets are displayed newest to oldest, and then new widgets appear above the old ones. New widgets act similarly to how they do in popup mode, where they are interactive for a limited time, but they do not disappear in timeline mode. Old widgets are not interactive.  Each "page" of widgets in the timeline contain up to the 20 most recent widgets. If there are more than 20 past widgets available, there will be a customisable "Load More" button at the end of the widget list that will load up to the next 20 widgets at a time. 

```html
<livelike-widgets programid="example-program-id" mode="timeline">
</livelike-widgets>
```

> 📘 Timeline Mode Deprection
>
> Note: Timeline mode has been deprecated and its support will be removed from next major release. Integrators should prefer using Interactive Timeline for their integrations

## Interactive Timeline Mode

In interactive timeline mode, 

* previously published widgets are displayed newest to oldest 
* then new widgets appear above the old ones. 
* All the widgets are interactive for infinite time. There is **no timer** attached to any of the widgets.  
* Each "page" of widgets in the timeline contain up to the 20 most recent widgets. 
* If there are more than 20 past widgets available, there will be a customisable "Load More" button at the end of the widget list that will load up to the next 20 widgets at a time. 

*Quiz Widgets*\
Quiz answers can be submitted by clicking on Vote button as there is no timer to initiate the answer submission\
*Slider Widgets*\
Slider votes an be submitted by clicking on Vote button as there is no timer to initiate the answer submission

```html
<livelike-widgets programid="example-program-id" mode="interactive-timeline">
</livelike-widgets>
```

Integrator can also control the timer on widgets in the Intractable timeline using method `overRideTimer`

Integrators can pass their own custom timer value or use the value received from CMS in widgetPayload\
(Note: widgetPayload.timeout should be converted into milliseconds before returning from this function)

The below code sample shows how we can implement a custom timer value in interactive-timeline.

```javascript
const widgets = document.querySelector('livelike-widgets');
let send15sTimer = ({widget}) => 15000 //Timer value should be in milliseconds
widgets && (widgets.overRideTimer = send15sTimer);
```

## Filtering Widgets

Integrators can filter published widgets from appearing on the timeline by using the following methods `onInitialWidgetsLoaded` and `onMoreWidgetsLoaded`\
Integrators can also filter widgets coming from CMS in real-time by using method `onWidgetReceived`

The sample code below filters all Alert Widgets from being displayed

```javascript
//For filtering old widgets (received from timeline resource)
const widgets = document.querySelector('livelike-widgets');
let filterAlertWidgets = ({widgets}) => widgets.filter(widget => widget.kind !== 'alert')
widgets && (widgets.onInitialWidgetsLoaded = filterAlertWidgets);
widgets && (widgets.onMoreWidgetsLoaded = filterAlertWidgets);

//For filtering new widgets (received from CMS via pubnub)
const widgets = document.querySelector('livelike-widgets');
let filterAlertWidgets = (widgetPayload) => widgetPayload.kind !== 'alert' && widgetPayload
widgets && (widgets.onWidgetReceived = filterAlertWidgets);
```

## Showing a Loader

When the livelike-widgets element is loading, it will render a `widgets-loading` slot. To use this, you can add any element as a child of livelike-widgets with the `slot="widgets-loading"` attribute.

```html
<livelike-widgets programid="example-program-id"  mode="timeline">
  <div slot="widgets-loading">Widgets loading...</div>
</livelike-widgets>
```

## Timeline Widget Bylines

Timeline mode can be used to implement things like [Live Blogs](doc:live-blog-tutorial)  and pinned widgets. Optionally, the widget author and timestamp bylines can be displayed with each widget. The author is the name of the user that created the widget, and the timestamp is the time when the widget was posted. One or both can be used, and it's as simple as adding them as attributes to the `<livelike-widgets>` element.

```text
<livelike-widgets programid="example-program-id" mode="timeline" authors timestamps></livelike-widgets>
```

Here is an example of the timeline mode with the bylines enabled.

<Embed url="https://codesandbox.io/s/flamboyant-galileo-he7st" title="flamboyant-galileo-he7st" favicon="null" image="https://codesandbox.io/api/v1/sandboxes/he7st/screenshot.png" provider="codesandbox.io" href="https://codesandbox.io/s/flamboyant-galileo-he7st" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fcodesandbox.io%252Fembed%252Fflamboyant-galileo-he7st%26url%3Dhttps%253A%252F%252Fcodesandbox.io%252Fs%252Fflamboyant-galileo-he7st%26image%3Dhttps%253A%252F%252Fcodesandbox.io%252Fapi%252Fv1%252Fsandboxes%252Fhe7st%252Fscreenshot.png%26key%3D02466f963b9b4bb8845a05b53d3235d7%26type%3Dtext%252Fhtml%26schema%3Dcodesandbox%22%20width%3D%221000%22%20height%3D%22500%22%20scrolling%3D%22no%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />

## Custom Mode Creation

If you need finer control over the widget lifecycle, a custom mode can be created using the [`registerWidgetMode` method](https://websdk.livelikecdn.com/docs/2.0.0/index.html#widgets)

The `registerWidgetMode` method's first argument is a string, the name of the mode to be used as the `mode` attribute on the livelike-widgets element, and the second argument is a function that has the `widgetPayload` object as an argument, and should return the widget lifecycle changes.

Below is an example of how to create your own timeline mode using the available methods.

**Custom timeline mode**

<Embed url="https://jsfiddle.net/livelike_web/dy6nthgv/1/" title="JSFiddle" favicon="https://jsfiddle.net/img/favicon.png" image="https://www.gravatar.com/avatar/086723cfa3c157182f68c30f0838f08c?s=80" provider="jsfiddle.net" href="https://jsfiddle.net/livelike_web/dy6nthgv/1/" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fjsfiddle.net%252Flivelike_web%252Fdy6nthgv%252Fembedded%252F%26display_name%3DjsFiddle%26url%3Dhttps%253A%252F%252Fjsfiddle.net%252Flivelike_web%252Fdy6nthgv%252F1%252F%26image%3Dhttps%253A%252F%252Fwww.gravatar.com%252Favatar%252F086723cfa3c157182f68c30f0838f08c%253Fs%253D80%26key%3Df2aa6fc3595946d0afc3d76cbbd25dc3%26type%3Dtext%252Fhtml%26schema%3Djsfiddle%22%20width%3D%22600%22%20height%3D%22400%22%20scrolling%3D%22no%22%20title%3D%22jsFiddle%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />
