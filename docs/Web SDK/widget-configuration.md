---
title: Widget Configuration
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widget Configuration | Web SDK | LiveLike
  description: >-
    Widget elements are composted of multiple building block elements that can
    be matched, styled, and composed.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: custom-widget-creation
      title: Custom Widget Creation
    - type: basic
      slug: custom-widget-examples
      title: Custom Widget Examples
---
[block:callout]
{
  "type": "warning",
  "title": "Only available in Web SDK version 2.0.0 and up."
}
[/block]

[block:api-header]
{
  "title": "Widget elements"
}
[/block]
Widget elements are composed of multiple "building block" elements. These elements are available to be mixed and matched, styled, and composed into unique experiences.

These elements can make use of content created and sent through our API, data from your own sources, or displayed anywhere as static elements.

For a full breakdown of all available elements and their properties, see the [API reference documentation.](https://websdk.livelikecdn.com/docs/2.0.0/elements.html)

For example, here is the markup of a text poll, with a breakdown explaining each tag.
[block:code]
{
  "codes": [
    {
      "code": "<template kind=\"image-poll\">\n  <livelike-widget-root>\n    <livelike-widget-header>\n      <livelike-title></livelike-title>\n      <livelike-timer></livelike-timer>\n      <livelike-dismiss-button></livelike-dismiss-button>\n    </livelike-widget-header>\n    <livelike-widget-body>\n      <livelike-select>\n        <template>\n          <livelike-option>\n            <livelike-description></livelike-description>\n            <livelike-progress></livelike-progress>\n            <livelike-percentage></livelike-percentage>\n            <livelike-image></livelike-image>\n          </livelike-option>\n        </template>\n      </livelike-select>\n    </livelike-widget-body>\n  </livelike-widget-root>\n</template>",
      "language": "html"
    }
  ]
}
[/block]
1. **template**
Each custom widget must be wrapped in a template element with a "kind" attribute that is the widget kind. This is to let the SDK know that the markup inside template should be rendered when that kind of widget is published. 

2. **livelike-widget-root**
A container, useful for composition. Has a `header`, `timer`, and `body` slot, as well as an unnamed slot for anything else.

3. **livelike-widget-header**
A container, useful for composition. Has a `title` and `dismiss-button` slot,  as well as an unnamed slot for anything else.

4. **livelike-title**
Renders the widget's `title` or `question` widget property.

5. **livelike-timer**
Renders a timer with the `timeout` property that is the widget's duration in milliseconds.

6. **livelike-dismiss-button**
Renders a button that fires the `dismissclicked` event, and 'dismisses' the widget.

7. **livelike-widget-body**
A container, useful for composition. Has an unnamed slot.

8. **livelike-select**
Takes a template element as a child, and renders the template content as a list per `options`/`choices` array item. For example, a Text Poll widget is published with two options. As a child of the livelike-select, we have a template with an livelike-option as the content. When the Text Poll gets rendered, two livelike-option elements will get rendered as a direct child of the livelike-select, one for each item in the `options` array. 

[block:code]
{
  "codes": [
    {
      "code": "// widgetPayload data with two `options` items.\nwidgetPayload : {\n  options: [\n    {description: 'Option One'},\n    {description: 'Option Two')\n  ]\n}\n\n// Template\n<template kind=\"text-poll\">\n  <livelike-select>\n    <template>\n      <livelike-option>\n        <livelike-description></livelike-description>\n      </livelike-option>\n    </template>\n  </livelike-select>\n</template>\n\n// What gets rendered\n<livelike-text-poll>\n  <livelike-select>\n    <livelike-option>\n      <livelike-description>Option One</livelike-description>\n    </livelike-option>\n    <livelike-option>\n      <livelike-description>Option Two</livelike-description>\n    </livelike-option>\n  </livelike-select>\n</livelike-text-poll>",
      "language": "html",
      "name": "Custom Template Rendered"
    }
  ]
}
[/block]
9. **template**
livelike-select child

10. **livelike-option**
Container component that contains an `option` or `choice` property from the `options`/`choices` array. Click listener is attached that sends vote on click.

11. **livelike-description**
Renders `description` property from `options`/`choices` array item.

13. **livelike-percentage**
Calculates percentage of votes in current `option`/`'choices` out of all votes in `options`/`choices` array.

12. **livelike-progress**
Calculates same percentage as livelike-percentage>

13. **livelike-image**
Renders `image_url` property from `options`/`choices` array item. Takes optional `src`, `height`, `width` attributes to override default.
[block:api-header]
{
  "title": "Styling Widgets"
}
[/block]
Widgets can be styled with CSS directly. Each of these building block elements has one job, either as a structural container or to render a widget property, and this allows for styling and recomposing. 

Different elements can be specified on a per widget basis, and custom element styles can be included alongside livelike element styles.

[block:code]
{
  "codes": [
    {
      "code": "<style>\nlivelike-text-poll livelike-widget-header {\n  padding: 1rem;  \n  color: white;\n}\nlivelike-text-poll livelike-title {\n  font-size: 24px;  \n}\nlivelike-text-poll .custom-subtitle {\n  font-size: 16px;\n}\nlivelike-text-poll livelike-widget-body {\n  background: grey;  \n}\nlivelike-text-poll livelike-option {\n  border: 1px solid blue;  \n}\nlivelike-text-poll livelike-description {\n  font-size: 20px;\n  color: white;\n}\n</style>\n\n<template kind=\"text-poll\">\n  <livelike-widget-header>\n    <livelike-title></livelike-title>\n    <h4 class=\"custom-subtitle\">Subtitle</h4>\n  </livelike-widget-header>\n  <livelike-widget-body>\n    <livelike-widget-select>\n      <template>\n        <livelike-option>\n          <livelike-description></livelike-description>\n        </livelike-option>\n      </template>\n    </livelike-widget-select>\n  </livelike-widget-body>\n</template>",
      "language": "html",
      "name": "Widget styling"
    }
  ]
}
[/block]