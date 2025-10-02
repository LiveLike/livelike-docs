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

To get started, you'll first need a program to publish widgets to. Every program has a unique <Glossary>Program ID</Glossary> that identifies it, and is used to configure the integration codes. Every widget published within that program will appear in your live blog, newest to oldest, when the page loads. New widgets will appear in the live blog as they are published without having to reload the page. Old widgets won't be interactive, but new ones will!

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

<Embed url="https://codepen.io/changdeo-livelike/pen/RwOJvzV" title="Widget Author and Timestamp" image="https://shots.codepen.io/username/pen/RwOJvzV-512.jpg?version=1712934971" provider="codepen.io" href="https://codepen.io/changdeo-livelike/pen/RwOJvzV" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fcodepen.io%252Fchangdeo-livelike%252Fembed%252Fpreview%252FRwOJvzV%253Fdefault-tabs%253Dhtml%25252Cresult%2526height%253D600%2526host%253Dhttps%25253A%25252F%25252Fcodepen.io%2526slug-hash%253DRwOJvzV%26display_name%3DCodePen%26url%3Dhttps%253A%252F%252Fcodepen.io%252Fchangdeo-livelike%252Fpen%252FRwOJvzV%26image%3Dhttps%253A%252F%252Fshots.codepen.io%252Fusername%252Fpen%252FRwOJvzV-512.jpg%253Fversion%253D1712934971%26key%3D7788cb384c9f4d5dbbdbeffd9fe4b92f%26type%3Dtext%252Fhtml%26schema%3Dcodepen%22%20width%3D%22800%22%20height%3D%22600%22%20scrolling%3D%22no%22%20title%3D%22CodePen%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" />
