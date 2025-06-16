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
> 🚧 Only available in Web SDK version 2.0.0 and up.

## Widget elements

Widget elements are composed of multiple "building block" elements. These elements are available to be mixed and matched, styled, and composed into unique experiences.

These elements can make use of content created and sent through our API, data from your own sources, or displayed anywhere as static elements.

For a full breakdown of all available elements and their properties, see the [API reference documentation.](https://websdk.livelikecdn.com/docs/2.0.0/elements.html)

For example, here is the markup of a text poll, with a breakdown explaining each tag.

```html
<template kind="image-poll">
  <livelike-widget-root>
    <livelike-widget-header>
      <livelike-title></livelike-title>
      <livelike-timer></livelike-timer>
      <livelike-dismiss-button></livelike-dismiss-button>
    </livelike-widget-header>
    <livelike-widget-body>
      <livelike-select>
        <template>
          <livelike-option>
            <livelike-description></livelike-description>
            <livelike-progress></livelike-progress>
            <livelike-percentage></livelike-percentage>
            <livelike-image></livelike-image>
          </livelike-option>
        </template>
      </livelike-select>
    </livelike-widget-body>
  </livelike-widget-root>
</template>
```

1. **template**\
   Each custom widget must be wrapped in a template element with a "kind" attribute that is the widget kind. This is to let the SDK know that the markup inside template should be rendered when that kind of widget is published. 

2. **livelike-widget-root**\
   A container, useful for composition. Has a `header`, `timer`, and `body` slot, as well as an unnamed slot for anything else.

3. **livelike-widget-header**\
   A container, useful for composition. Has a `title` and `dismiss-button` slot,  as well as an unnamed slot for anything else.

4. **livelike-title**\
   Renders the widget's `title` or `question` widget property.

5. **livelike-timer**\
   Renders a timer with the `timeout` property that is the widget's duration in milliseconds.

6. **livelike-dismiss-button**\
   Renders a button that fires the `dismissclicked` event, and 'dismisses' the widget.

7. **livelike-widget-body**\
   A container, useful for composition. Has an unnamed slot.

8. **livelike-select**\
   Takes a template element as a child, and renders the template content as a list per `options`/`choices` array item. For example, a Text Poll widget is published with two options. As a child of the livelike-select, we have a template with an livelike-option as the content. When the Text Poll gets rendered, two livelike-option elements will get rendered as a direct child of the livelike-select, one for each item in the `options` array. 

```html Custom Template Rendered
// widgetPayload data with two `options` items.
widgetPayload : {
  options: [
    {description: 'Option One'},
    {description: 'Option Two')
  ]
}

// Template
<template kind="text-poll">
  <livelike-select>
    <template>
      <livelike-option>
        <livelike-description></livelike-description>
      </livelike-option>
    </template>
  </livelike-select>
</template>

// What gets rendered
<livelike-text-poll>
  <livelike-select>
    <livelike-option>
      <livelike-description>Option One</livelike-description>
    </livelike-option>
    <livelike-option>
      <livelike-description>Option Two</livelike-description>
    </livelike-option>
  </livelike-select>
</livelike-text-poll>
```

9. **template**\
   livelike-select child

10. **livelike-option**\
    Container component that contains an `option` or `choice` property from the `options`/`choices` array. Click listener is attached that sends vote on click.

11. **livelike-description**\
    Renders `description` property from `options`/`choices` array item.

12. **livelike-percentage**\
    Calculates percentage of votes in current `option`/`'choices` out of all votes in `options`/`choices` array.

13. **livelike-progress**\
    Calculates same percentage as livelike-percentage>

14. **livelike-image**\
    Renders `image_url` property from `options`/`choices` array item. Takes optional `src`, `height`, `width` attributes to override default.

## Styling Widgets

Widgets can be styled with CSS directly. Each of these building block elements has one job, either as a structural container or to render a widget property, and this allows for styling and recomposing. 

Different elements can be specified on a per widget basis, and custom element styles can be included alongside livelike element styles.

```html Widget styling
<style>
livelike-text-poll livelike-widget-header {
  padding: 1rem;  
  color: white;
}
livelike-text-poll livelike-title {
  font-size: 24px;  
}
livelike-text-poll .custom-subtitle {
  font-size: 16px;
}
livelike-text-poll livelike-widget-body {
  background: grey;  
}
livelike-text-poll livelike-option {
  border: 1px solid blue;  
}
livelike-text-poll livelike-description {
  font-size: 20px;
  color: white;
}
</style>

<template kind="text-poll">
  <livelike-widget-header>
    <livelike-title></livelike-title>
    <h4 class="custom-subtitle">Subtitle</h4>
  </livelike-widget-header>
  <livelike-widget-body>
    <livelike-widget-select>
      <template>
        <livelike-option>
          <livelike-description></livelike-description>
        </livelike-option>
      </template>
    </livelike-widget-select>
  </livelike-widget-body>
</template>
```
