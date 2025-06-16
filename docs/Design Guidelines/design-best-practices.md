---
title: Layout Best Practices
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Layout Best Practices | Design Guidelines | LiveLike
  description: >-
    Chat and Widgets are meant to augment the video watching experience. Learn
    more about layout Best Practices to optimize your content.
  robots: index
next:
  description: ''
---
Chat and Widgets are meant to augment the video watching experience. This page explores Best Practices to make sure it doesn't get in the way of the content. This is mostly a challenge on Mobile and we will suggest best practices.

## Usage observations

Most people prefer to watch 16:9 videos in landscape. Only when they jump into the chat will many switch momentarily to portrait to use a more natural keyboard layout. Focusing on the landscape layout is therefore important.

# Chat
## Great fit with new aspect ratios

Mobile screen sizes have changed radically in 2019. In 2020, most phones won't be 16:9 in aspect ratio (although this varies per territory).
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e2a99fd-Mobile-aspect-ratios.jpg",
        "Mobile-aspect-ratios.jpg",
        1236,
        782,
        "#fafafa"
      ],
      "caption": "Aspect ratio of Smartphones\nUS Data from Statcounter.com"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5b43616-Pillarboxing-vs-Cropped.gif",
        "Pillarboxing-vs-Cropped.gif",
        600,
        277,
        "#49454e"
      ],
      "caption": "Recent phones (iPhone X and more recent) have aspect ration superior to 16:9 leaving you with the choice to crop or pillarbox videos",
      "sizing": "full"
    }
  ]
}
[/block]
On mobile, people want to maximize screen estate: pillarboxing is not the best way to maximize screen estate and cropping video is often undesirable. With most recent smartphones featuring aspect ratios between 2 and 2,15, this gives you enough room to add chat while actually maximizing screen estate.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6bad769-Show-Chat.gif",
        "Show-Chat.gif",
        600,
        277,
        "#49454d"
      ],
      "caption": "Using a narrow chat maximizes overall screen estate with little trade offs"
    }
  ]
}
[/block]
Especially keeping in mind older devices that are 16:9, avoid too large a chat as it will increase significantly the letterboxing.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c090689-Chat-size-30vs40.gif",
        "Chat-size-30vs40.gif",
        600,
        277,
        "#6c6a72"
      ],
      "caption": "30% vs 40% width -- a narrow chat is harder design constraint but ensures chat supports the video experience and doesn't take away from it.",
      "sizing": "full"
    }
  ]
}
[/block]
## Give user choices
To appeal to a broad audience you'll need to offer choices. Users under 35 respond very positively to chat & widgets, while users above 35 are more likely to want a way to hide chat or widgets.

Consider how you can integrate controls to show and hide chat in a natural and clear way into your video controls. The example below is just food for thought about how you could offer different viewing options:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/849cc52-Layout-options.gif",
        "Layout-options.gif",
        600,
        325,
        "#7d7b81"
      ],
      "caption": "An example of different viewing options that could be offered to users"
    }
  ]
}
[/block]
Get creative and consider the following matrix of viewing options:
[block:parameters]
{
  "data": {
    "0-0": "1. Chat as tray",
    "1-0": "2. Chat as overlay",
    "2-0": "3. No chat",
    "h-1": "Video cropped: OFF",
    "h-2": "Video cropped: ON",
    "0-1": "**Chat tray with letterboxing**\nRecommended as default view.",
    "0-2": "**Chat tray with no letterboxing**",
    "1-1": "**Overlay + Tray**\nConsider fading out chat above 50% in height. \n\nConsider if a navigation sidebar can facilitate navigation of ancillary content (chat, stats...)",
    "2-1": "**No chat + Tray**\nConsider if a navigation sidebar can facilitate navigation of ancillary content (chat, stats...)",
    "1-2": "**Overlay + No tray**\nKeeping the chat as overlay but no side-menu.",
    "2-2": "**No chat + No Tray**\nTaking advantage of the full width.",
    "h-0": "Viewing mode"
  },
  "cols": 3,
  "rows": 3
}
[/block]

[block:api-header]
{
  "title": "Widgets"
}
[/block]
Much like chat, widgets should complement the video content and not take away from it.
Consider ways to overlay widgets in the least intrusive ways possible. If overlaying it on the video consider using a lower third placement. Consider also pop-in widgets on top of chat.