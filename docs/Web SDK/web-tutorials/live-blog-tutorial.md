---
title: Live Blog Tutorial
excerpt: Using Timeline Mode to implement a live blog
deprecated: false
hidden: false
metadata:
  title: Live Blog Tutorial | Web SDK | LiveLike Developer Hub
  description: >-
    The Web SDK has two built-in widget timeline modes. Learn about using
    timeline mode to implement a live blog.
  robots: index
next:
  description: ''
---
The Web SDK has two built-in widget Timeline modes. A great use case for the Timeline Mode is to show a live blog. When a page with a live blog on it loads, all the widgets published to that page will load oldest to newest.

In the `timeline` mode, the list of widgets that are initially loaded will not be interactive. New widgets that are published will be interactive, and they will appear at the top of the timeline without needing to reload the page.

> 👍 Timeline Mode is available version 1.3 and later
> 
> Timeline Mode was added in Web SDK version 1.3, and was extended with author and timestamp displays in 1.4.

In the `interactive-timeline` mode, all widgets that load will be interactive. 

> 👍 Interactive Timeline Mode is available version 2.5.0 and later

A great use case for the Timeline Mode for widgets is to show a live blog. When a page with a live blog on it loads, all the widgets published to that page will load oldest to newest but they won't be interactive. New widgets will be interactive though and they will appear at the top of the timeline without having to reload the page.

## Step 1. Create a program

To get started, you'll first need a program to publish widgets to. Every program has a unique <<glossary:Program ID>> that identifies it, and is used to configure the integration codes. Every widget published within that program will appear in your live blog, newest to oldest, when the page loads. New widgets will appear in the live blog as they are published without having to reload the page. Old widgets won't be interactive, but new ones will!

## Step 2. Embed the live blog on your page

Using the program ID from step one to place the `<livelike-widgets>` where the live blog should appear. The key is the `mode="timeline"` attribute, which changes the default behavior of the widget element from popup to timeline mode. Popup mode has new widgets appear for a short amount of time before disappearing. Timeline mode causes widgets to stack up and remain on the page, and won't disappear.

```html
<livelike-widgets programid="your-program-id" mode="timeline">
</livelike-widgets>
```

Changing the `mode` attribute to `interactive-timeline` will make all widgets interactive by default.

```html
<livelike-widgets programid="your-program-id" mode="interactive-timeline">
</livelike-widgets>
```

## Step 3. Timestamps

The time each widget was published can be displayed with the `timestamps` attribute.

```html
<livelike-widgets programid="your-program-id" mode="interactive-timeline" timestamps>
</livelike-widgets>
```

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fcodepen.io%2Fchangdeo-livelike%2Fembed%2Fpreview%2FRwOJvzV%3Fdefault-tabs%3Dhtml%252Cresult%26height%3D600%26host%3Dhttps%253A%252F%252Fcodepen.io%26slug-hash%3DRwOJvzV&display_name=CodePen&url=https%3A%2F%2Fcodepen.io%2Fchangdeo-livelike%2Fpen%2FRwOJvzV&image=https%3A%2F%2Fshots.codepen.io%2Fusername%2Fpen%2FRwOJvzV-512.jpg%3Fversion%3D1712934971&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=codepen\" width=\"800\" height=\"600\" scrolling=\"no\" title=\"CodePen embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://codepen.io/changdeo-livelike/pen/RwOJvzV",
  "title": "Widget Author and Timestamp",
  "image": "https://shots.codepen.io/username/pen/RwOJvzV-512.jpg?version=1712934971",
  "provider": "https://codepen.io",
  "href": "https://codepen.io/changdeo-livelike/pen/RwOJvzV"
}
[/block]