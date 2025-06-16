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
[block:api-header]
{
  "title": "Popup Mode"
}
[/block]
Widgets appear for a limited time and then disappear. They are interactive until the timer animation runs out. It is typically used for live interactive experiences.
[block:code]
{
  "codes": [
    {
      "code": "<!-- The mode attribute is optional and defaults to popup -->\n<livelike-widgets programid=\"example-program-id\" mode=\"pop-up\">\n</livelike-widgets>",
      "language": "html"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Timeline Mode"
}
[/block]
Previously published widgets are displayed newest to oldest, and then new widgets appear above the old ones. New widgets act similarly to how they do in popup mode, where they are interactive for a limited time, but they do not disappear in timeline mode. Old widgets are not interactive.  Each "page" of widgets in the timeline contain up to the 20 most recent widgets. If there are more than 20 past widgets available, there will be a customisable "Load More" button at the end of the widget list that will load up to the next 20 widgets at a time. 
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets programid=\"example-program-id\" mode=\"timeline\">\n</livelike-widgets>",
      "language": "html"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Note: Timeline mode has been deprecated and its support will be removed from next major release. Integrators should prefer using Interactive Timeline for their integrations",
  "title": "Timeline Mode Deprection"
}
[/block]

[block:api-header]
{
  "title": "Interactive Timeline Mode"
}
[/block]
In interactive timeline mode, 
* previously published widgets are displayed newest to oldest 
* then new widgets appear above the old ones. 
* All the widgets are interactive for infinite time. There is **no timer** attached to any of the widgets.  
* Each "page" of widgets in the timeline contain up to the 20 most recent widgets. 
* If there are more than 20 past widgets available, there will be a customisable "Load More" button at the end of the widget list that will load up to the next 20 widgets at a time. 

*Quiz Widgets*
Quiz answers can be submitted by clicking on Vote button as there is no timer to initiate the answer submission
*Slider Widgets*
Slider votes an be submitted by clicking on Vote button as there is no timer to initiate the answer submission
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets programid=\"example-program-id\" mode=\"interactive-timeline\">\n</livelike-widgets>",
      "language": "html"
    }
  ]
}
[/block]
Integrator can also control the timer on widgets in the Intractable timeline using method `overRideTimer`

Integrators can pass their own custom timer value or use the value received from CMS in widgetPayload 
(Note: widgetPayload.timeout should be converted into milliseconds before returning from this function)

The below code sample shows how we can implement a custom timer value in interactive-timeline.
[block:code]
{
  "codes": [
    {
      "code": "const widgets = document.querySelector('livelike-widgets');\nlet send15sTimer = ({widget}) => 15000 //Timer value should be in milliseconds\nwidgets && (widgets.overRideTimer = send15sTimer);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Filtering Widgets"
}
[/block]
Integrators can filter published widgets from appearing on the timeline by using the following methods `onInitialWidgetsLoaded` and `onMoreWidgetsLoaded`
Integrators can also filter widgets coming from CMS in real-time by using method `onWidgetReceived`

The sample code below filters all Alert Widgets from being displayed
[block:code]
{
  "codes": [
    {
      "code": "//For filtering old widgets (received from timeline resource)\nconst widgets = document.querySelector('livelike-widgets');\nlet filterAlertWidgets = ({widgets}) => widgets.filter(widget => widget.kind !== 'alert')\nwidgets && (widgets.onInitialWidgetsLoaded = filterAlertWidgets);\nwidgets && (widgets.onMoreWidgetsLoaded = filterAlertWidgets);\n\n//For filtering new widgets (received from CMS via pubnub)\nconst widgets = document.querySelector('livelike-widgets');\nlet filterAlertWidgets = (widgetPayload) => widgetPayload.kind !== 'alert' && widgetPayload\nwidgets && (widgets.onWidgetReceived = filterAlertWidgets);",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Showing a Loader"
}
[/block]
When the livelike-widgets element is loading, it will render a `widgets-loading` slot. To use this, you can add any element as a child of livelike-widgets with the `slot="widgets-loading"` attribute.
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets programid=\"example-program-id\"  mode=\"timeline\">\n  <div slot=\"widgets-loading\">Widgets loading...</div>\n</livelike-widgets>",
      "language": "html"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Timeline Widget Bylines"
}
[/block]
Timeline mode can be used to implement things like [Live Blogs](doc:live-blog-tutorial)  and pinned widgets. Optionally, the widget author and timestamp bylines can be displayed with each widget. The author is the name of the user that created the widget, and the timestamp is the time when the widget was posted. One or both can be used, and it's as simple as adding them as attributes to the `<livelike-widgets>` element.
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets programid=\"example-program-id\" mode=\"timeline\" authors timestamps></livelike-widgets>",
      "language": "text"
    }
  ]
}
[/block]
Here is an example of the timeline mode with the bylines enabled.
[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fcodesandbox.io%2Fembed%2Fflamboyant-galileo-he7st&url=https%3A%2F%2Fcodesandbox.io%2Fs%2Fflamboyant-galileo-he7st&image=https%3A%2F%2Fcodesandbox.io%2Fapi%2Fv1%2Fsandboxes%2Fhe7st%2Fscreenshot.png&key=02466f963b9b4bb8845a05b53d3235d7&type=text%2Fhtml&schema=codesandbox\" width=\"1000\" height=\"500\" scrolling=\"no\" frameborder=\"0\" allow=\"autoplay; fullscreen\" allowfullscreen=\"true\"></iframe>",
  "url": "https://codesandbox.io/s/flamboyant-galileo-he7st",
  "title": "flamboyant-galileo-he7st",
  "favicon": null,
  "image": "https://codesandbox.io/api/v1/sandboxes/he7st/screenshot.png"
}
[/block]

[block:api-header]
{
  "title": "Custom Mode Creation"
}
[/block]
If you need finer control over the widget lifecycle, a custom mode can be created using the [`registerWidgetMode` method](https://websdk.livelikecdn.com/docs/2.0.0/index.html#widgets)

The `registerWidgetMode` method's first argument is a string, the name of the mode to be used as the `mode` attribute on the livelike-widgets element, and the second argument is a function that has the `widgetPayload` object as an argument, and should return the widget lifecycle changes.


Below is an example of how to create your own timeline mode using the available methods.

**Custom timeline mode**
[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fjsfiddle.net%2Flivelike_web%2Fdy6nthgv%2Fembedded%2F&display_name=jsFiddle&url=https%3A%2F%2Fjsfiddle.net%2Flivelike_web%2Fdy6nthgv%2F1%2F&image=https%3A%2F%2Fwww.gravatar.com%2Favatar%2F086723cfa3c157182f68c30f0838f08c%3Fs%3D80&key=f2aa6fc3595946d0afc3d76cbbd25dc3&type=text%2Fhtml&schema=jsfiddle\" width=\"600\" height=\"400\" scrolling=\"no\" title=\"jsFiddle embed\" frameborder=\"0\" allow=\"autoplay; fullscreen\" allowfullscreen=\"true\"></iframe>",
  "url": "https://jsfiddle.net/livelike_web/dy6nthgv/1/",
  "title": "JSFiddle",
  "favicon": "https://jsfiddle.net/img/favicon.png",
  "image": "https://www.gravatar.com/avatar/086723cfa3c157182f68c30f0838f08c?s=80"
}
[/block]