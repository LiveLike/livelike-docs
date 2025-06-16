---
title: Chat Message Timestamps
excerpt: Customizing chat message timestamps on web
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Web Version 1.8+ is required

## Showing Timestamps

Chat messages do not show timestamps by default. Add the `timestamps` bare attribute to the chat element to enable them:


[block:embed]
{
  "html": false,
  "url": "https://codepen.io/tanyalivelike/embed/XWgMwJG",
  "href": "https://codepen.io/tanyalivelike/pen/XWgMwJG",
  "typeOfEmbed": "iframe",
  "height": "300px",
  "width": "100%",
  "iframe": true,
  "provider": "embed"
}
[/block]




The timestamp formatter will respect the [lang](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang) attribute if it is present, so timestamps will appear localized. The language will default to `"en"` if it is undefined.

## Formatting Timestamps

The timestamp format can be changed by setting the `timeFormat` property on the chat node. The `timeFormat` value should be an object in the same format as the options to [Date.toLocaleDateString](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleDateString).