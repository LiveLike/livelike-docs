---
title: YouTube Live Integration
excerpt: How to use LiveLike with an embedded YouTube Live player on your page
deprecated: false
hidden: false
metadata:
  title: YouTube Live Integration | Web SDK | Web Tutorial | LiveLike
  description: >-
    Integrating LiveLike and YouTube Live can be done right on your own pages
    using HTML embed codes. Learn about YouTube Live Integration.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: getting-started-with-the-web-sdk
      title: Getting Started
    - type: basic
      slug: web-widgets
      title: Widgets
    - type: basic
      slug: live-blog-tutorial
      title: Live Blog Tutorial
    - type: link
      title: Streaming a Zoom Meeting or Webinar to YouTube Live
      url: >-
        https://support.zoom.us/hc/en-us/articles/360028478292-Streaming-a-Meeting-or-Webinar-on-YouTube-Live
---
Integrating LiveLike and YouTube Live can be done right on your own pages using HTML embed codes. Both LiveLike and YouTube support embedding their contents directly onto your page by copying an *embed code* and then pasting it into the HTML on a page where you want it to appear. Follow the steps below to learn how to integrate LiveLike and YouTube Live onto your page.
[block:api-header]
{
  "title": "Step 1. Embed YouTube Live Player"
}
[/block]
The first step is to embed the YouTube Live Player for your channel on your page. To do that, you will need to get a copy of the embed code for your channel. The YouTube Live Dashboard makes this easy. Follow these steps to get the embed code from your dashboard:

* Make sure your live stream is either unlisted or public
* Navigate to your live watch page from https://www.youtube.com/live_dashboard
* Hit Share, then Embed, then copy the embed code
* Paste the embed code onto your page where you want the player to appear

Alternatively, if you know your Channel ID you can replace `CHANNEL_ID` in the example embed code below and paste into your page HTML:
[block:code]
{
  "codes": [
    {
      "code": "<iframe width=\"560\" height=\"315\" src=\"https://www.youtube.com/embed/live_stream?channel=CHANNEL_ID\" frameborder=\"0\" allowfullscreen></iframe>",
      "language": "html"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "Don't know your Channel ID?",
  "body": "You can find your Channel ID on this page https://www.youtube.com/account_advanced"
}
[/block]

[block:callout]
{
  "type": "info",
  "title": "Streaming from Zoom?",
  "body": "You can stream a Zoom meeting or webinar to YouTube Live. Check the [Streaming to YouTube Live section of the Zoom docs](https://support.zoom.us/hc/en-us/articles/360028478292-Streaming-a-Meeting-or-Webinar-on-YouTube-Live)."
}
[/block]

[block:api-header]
{
  "title": "Step 2. Embed LiveLike Widgets"
}
[/block]
The second step is to embed LiveLike widgets on your page. You will need two values:

1. Your application's <<glossary:Client ID>> 
2. Your program's <<glossary:Program ID>>

Please see [Retrieving Important Keys](doc:retrieving-important-keys) for details on how to obtain your Client ID and Program IDs. Replace `CLIENT_ID` in the embed code below and add it to your page. This only needs to be added once to a page, and usually goes near the bottom of the body tag:
[block:code]
{
  "codes": [
    {
      "code": "<script src=\"https://unpkg.com/@livelike/engagementsdk@1/livelike.umd.js\"></script>\n<script>LiveLike.init({ clientId: \"CLIENT_ID\" })</script>",
      "language": "html",
      "name": "Setup"
    }
  ]
}
[/block]
Replace  `PROGRAM_ID` with your Program ID in the embed code below, and then add it onto your page where you want widgets to appear:
[block:code]
{
  "codes": [
    {
      "code": "<livelike-widgets programid=\"PROGRAM_ID\"></livelike-widgets>",
      "language": "html",
      "name": "Widgets"
    }
  ]
}
[/block]
For more information about how to initialize and use the Web SDK, see [Getting Started on the Web](doc:getting-started-with-the-web-sdk).
[block:callout]
{
  "type": "info",
  "title": "Want to embed a live blog or chat room too?",
  "body": "See the [Web Embeds](doc:web-embeds) guide for how to embed more LiveLike features on your pages."
}
[/block]

[block:api-header]
{
  "title": "Step 3. Publish a Widget"
}
[/block]
Finally, it's time to test your integration to make sure it's working. Publish a widget from the Producer Suite to the program you embedded on your page. You should see it appear within a few seconds. Congratulations!