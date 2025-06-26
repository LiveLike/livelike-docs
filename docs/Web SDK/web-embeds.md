---
title: Web Embeds
excerpt: Embedding LiveLike features on your web pages
deprecated: false
hidden: false
metadata:
  title: Web Embeds | Fan Engagement | LiveLike Developer Hub
  description: >-
    Features like chat, watch parties, and other widgets can be added. to your
    web pages with HTML embed codes. Learn more.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: live-blog-tutorial
      title: Live Blog Tutorial
    - type: basic
      slug: youtube-live-integration-web-tutorial
      title: YouTube Live Integration
    - type: basic
      slug: custom-themes
      title: Custom Themes
---
Features like [Chat](doc:chat), [Widgets](doc:widgets), and more can be added to your web pages with HTML embed codes. Anywhere you can paste an HTML embed code, you can add LiveLike functionality.  These codes can be used in HTML files, or in popular web site builders, or your favorite blogging tool.

> 👍 Make sure you have a Client ID
>
> You'll need a Client ID to initialize the SDK. Check out [Retrieving Important Keys](doc:retrieving-important-keys) for instructions on how to get one.

## Setting Up

Add the snippet below onto your page only once. The ideal place to put it is at the bottom of the page, inside of the `<body>` tag. Replace `YOUR-CLIENT-ID` with your <Glossary>Client ID</Glossary> before saving your page.

```html
<script src="https://unpkg.com/@livelike/engagementsdk@2.54.0/livelike.umd.js"></script>
<script>LiveLike.init({ clientId: "YOUR-CLIENT-ID" });</script>
```

> 🚧
>
> This snippet only needs to be added once on your page, and then any number of LiveLike tags can be added.

## Timeline Widgets

Add the embed code below anywhere on your page to display [widgets in timeline mode](doc:web-widget-modes) wherever the code is placed. Replace `YOUR-PROGRAM-ID` with your event's <Glossary>Program ID</Glossary>.

```html
<livelike-widgets programid="YOUR-PROGRAM-ID" mode="timeline"></livelike-widgets>
```

> 📘 Making a live blog?
>
> Widgets in timeline mode can be used as a live blog. After you have widgets appearing on your site, you can customize your integration even further with CSS. Check out the [Live Blog Tutorial](doc:live-blog-tutorial) for more information.

## Pop-up Widgets

Add the embed code below anywhere on your page to display [pop-up widgets](doc:web-widget-modes) wherever the code is placed. Replace `YOUR-PROGRAM-ID` with your event's <Glossary>Program ID</Glossary>.

```html
<livelike-widgets programid="YOUR-PROGRAM-ID"></livelike-widgets>
```

## Chat Rooms

Add the embed code below anywhere to your page to display a chat room on your page.

```html HTML
<livelike-chat roomid="YOUR-ROOM-ID"></livelike-chat>
```

## Embedded Individual Widgets

Integrators can embed any widget in their web page using their embed codes from the LiveLike CMS:

1. Navigate to the widget in the LiveLike CMS
2. Click on the "Embed" button
3. Copy the provided HTML code
4. Paste it into your web page

OR if you already have the widget id and widget kind/type, you could use the following code (for example embedding text quiz widget):

```html
<livelike-text-quiz widgetid="YOUR-WIDGET-ID"></livelike-text-quiz>
```

Below are the list of available widget web components:

| Widget Type                       | Web Component                              | Usage                                                                                                                 |
| --------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| Text Poll                         | livelike-text-poll                         | `<livelike-text-poll widgetid="YOUR-WIDGET-ID"></livelike-text-poll>`                                                 |
| Image Poll                        | livelike-image-poll                        | `<livelike-image-poll widgetid="YOUR-WIDGET-ID"></livelike-image-poll>`                                               |
| Text Quiz                         | livelike-text-quiz                         | `<livelike-text-quiz widgetid="YOUR-WIDGET-ID"></livelike-text-quiz>`                                                 |
| Image Quiz                        | livelike-image-quiz                        | `<livelike-image-quiz widgetid="YOUR-WIDGET-ID"></livelike-image-quiz>`                                               |
| Text Prediction                   | livelike-text-prediction                   | `<livelike-text-prediction widgetid="YOUR-WIDGET-ID"></livelike-text-prediction>`                                     |
| Text Prediction Follow-up         | livelike-text-prediction-follow-up         | `<livelike-text-prediction-follow-up widgetid="YOUR-WIDGET-ID"></livelike-text-prediction-follow-up>`                 |
| Image Prediction                  | livelike-image-prediction                  | `<livelike-image-prediction widgetid="YOUR-WIDGET-ID"></livelike-image-prediction>`                                   |
| Image Prediction Follow-up        | livelike-image-prediction-follow-up        | `<livelike-image-prediction-follow-up widgetid="YOUR-WIDGET-ID"></livelike-image-prediction-follow-up>`               |
| Cheer Meter                       | livelike-cheer-meter                       | `<livelike-cheer-meter widgetid="YOUR-WIDGET-ID"></livelike-cheer-meter>`                                             |
| Emoji Slider                      | livelike-emoji-slider                      | `<livelike-emoji-slider widgetid="YOUR-WIDGET-ID"></livelike-emoji-slider>`                                           |
| Rich Post                         | livelike-rich-post                         | `<livelike-rich-post widgetid="YOUR-WIDGET-ID"></livelike-rich-post>`                                                 |
| Social Embed                      | livelike-social-embed                      | `<livelike-social-embed widgetid="YOUR-WIDGET-ID"></livelike-social-embed>`                                           |
| Video Alert                       | livelike-video-alert                       | `<livelike-video-alert   widgetid="YOUR-WIDGET-ID"></livelike-video-alert>`                                           |
| Text Ask                          | livelike-text-ask                          | `<livelike-text-ask widgetid="YOUR-WIDGET-ID"></livelike-text-ask>`                                                   |
| Text Number Prediction            | livelike-text-number-prediction            | `<livelike-text-number-prediction widgetid="YOUR-WIDGET-ID"></livelike-text-number-prediction>`                       |
| Text Number Prediction Follow-up  | livelike-text-number-prediction-follow-up  | `<livelike-text-number-prediction-follow-up widgetid="YOUR-WIDGET-ID"></livelike-text-number-prediction-follow-up>`   |
| Image Number Prediction           | livelike-image-number-prediction           | `<livelike-image-number-prediction widgetid="YOUR-WIDGET-ID"></livelike-image-number-prediction>`                     |
| Image Number Prediction Follow-up | livelike-image-number-prediction-follow-up | `<livelike-image-number-prediction-follow-up widgetid="YOUR-WIDGET-ID"></livelike-image-number-prediction-follow-up>` |

**Replace`YOUR-WIDGET-ID` with your actual LiveLike Widget ID**

Any template added in HTML for the widget kind will be applied to embedded widgets

```html
<livelike-text-quiz widgetid="XXXXXXX"></livelike-text-quiz>
```
```html Embedded Widget with Custom Template
<template kind="text-quiz>
	....
</template>
<livelike-text-quiz widgetid="XXXXXXX"></livelike-text-quiz>
```

<br />

## Example: Complete Embed default widget Integration

```html
<!DOCTYPE html>
<html>
  <head>
    <title>LiveLike Integration Example</title>
    <style>
      :root {
        --livelike-primary-color: #0066ff;
        --livelike-text-color: #333333;
      }
      .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
        display: grid;
        grid-template-columns: 2fr 1fr;
        gap: 20px;
      }
      .widgets-container,
      .chat-container {
        border: 1px solid #eee;
        border-radius: 8px;
        padding: 15px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <livelike-text-quiz widgetid="YOUR-WIDGET-ID"></livelike-text-quiz>
    </div>

    <!-- LiveLike SDK -->
    <script src="https://unpkg.com/@livelike/[email protected]/livelike.umd.js"></script>
    <script>
      // Initialize the SDK
      LiveLike.init({
        clientId: 'YOUR-CLIENT-ID',
        // Optional: Add user identification
        user: {
          id: 'USER-ID',
          accessToken: 'USER-ACCESS-TOKEN',
        },
      });
    </script>
  </body>
</html>
```

<br />

### Embedded Custom Widgets

Custom Widgets can be embedded by adding the custom element created with the widget id.

```html
<script>
  class CustomAlert extends LiveLikeAlert {
    render() {
      return html`
        <template>
          <livelike-widget-root>
            <livelike-widget-header>
              <livelike-title></livelike-title>
              ${this.link_url &&
              html`
              <a href="${this.link_url}" target="_blank">${this.link_label}</a>
              `}
            </livelike-widget-header>
            <livelike-widget-body>
              <span>${this.text}</span>
              ${this.image_url &&
              html`
              <img src=${this.image_url} height="40px">
              `}
            </livelike-widget-body>
          </livelike-widget-root>
         <template>
      `;
      }
    }
  customElements.define("custom-alert", CustomAlert);
</script>
<custom-alert widgetid="XXXXXXX"></custom-alert>
```

Please note for custom Quiz, Polls, Predictions and Follow Ups, widget kind should be specified in the custom class

```javascript
class CustomImagePrediction extends LiveLikePrediction {
  connectedCallback() {
    this.kind = "image-prediction";
    super.connectedCallback();
  }
  render() {
    return html`
      <template>
        ...
      </template>
    `;
  }
}
```

## Embedded Individual Widgets via Custom Mode

If you need finer control over the widget lifecycle, a custom mode can be created using the [`registerWidgetMode` method](https://websdk.livelikecdn.com/docs/2.0.0/index.html#widgets)

The `registerWidgetMode` method's first argument is a string, the name of the mode to be used as the `mode` attribute on the widgets element, and the second argument is a function that has the `widgetPayload` object as an argument, and should return the widget lifecycle changes.

Below is an example of how to create your own timeline mode using the available methods.

<Embed url="https://codepen.io/abhi1599/pen/rNGeOqQ?editors=1010" href="https://codepen.io/abhi1599/pen/rNGeOqQ?editors=1010" html="%3Ciframe%20height%3D'350'%20scrolling%3D'no'%20src%3D'https%3A%2F%2Fcodepen.io%2Fabhi1599%2Fembed%2FrNGeOqQ%3Feditors%3D1010'%20frameborder%3D'no'%20allowtransparency%3D'true'%20allowfullscreen%3D'true'%20style%3D'width%3A%20100%25%3B'%3E%3C%2Fiframe%3E" />

## Troubleshooting

### I'm using a content management system to add the embed codes to my page, but they are not showing up. What's happening?

Some publishing tools automatically sanitize scripts and HTML that seem suspicious as a security measure. Try updating your tool's configuration to allow these tags to be added to your pages:

* `<livelike-widgets>`
* `<livelike-chat>`

### I'm using Squarespace. What's the best way to use LiveLike on my page?

You can use [Code Injection](https://support.squarespace.com/hc/en-us/articles/205815908) to add the code from "Setting Up" to your pages. You can use Squarespace's Per-Page Code Injection feature to add it on specific pages.

Once the setup code is on your page, you can embed as many widgets as you'd like, anywhere on your page. Use the [Code Block](https://support.squarespace.com/hc/en-us/articles/206543167) control to add LiveLike features.