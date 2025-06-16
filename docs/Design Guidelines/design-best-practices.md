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

<Image title="Mobile-aspect-ratios.jpg" alt={1236} src="https://files.readme.io/e2a99fd-Mobile-aspect-ratios.jpg">
  Aspect ratio of Smartphones\
  US Data from Statcounter.com
</Image>

<Image title="Pillarboxing-vs-Cropped.gif" alt={600} width="100%" src="https://files.readme.io/5b43616-Pillarboxing-vs-Cropped.gif">
  Recent phones (iPhone X and more recent) have aspect ration superior to 16:9 leaving you with the choice to crop or pillarbox videos
</Image>

On mobile, people want to maximize screen estate: pillarboxing is not the best way to maximize screen estate and cropping video is often undesirable. With most recent smartphones featuring aspect ratios between 2 and 2,15, this gives you enough room to add chat while actually maximizing screen estate.

<Image title="Show-Chat.gif" alt={600} src="https://files.readme.io/6bad769-Show-Chat.gif">
  Using a narrow chat maximizes overall screen estate with little trade offs
</Image>

Especially keeping in mind older devices that are 16:9, avoid too large a chat as it will increase significantly the letterboxing.

<Image title="Chat-size-30vs40.gif" alt={600} width="100%" src="https://files.readme.io/c090689-Chat-size-30vs40.gif">
  30% vs 40% width -- a narrow chat is harder design constraint but ensures chat supports the video experience and doesn't take away from it.
</Image>

## Give user choices

To appeal to a broad audience you'll need to offer choices. Users under 35 respond very positively to chat & widgets, while users above 35 are more likely to want a way to hide chat or widgets.

Consider how you can integrate controls to show and hide chat in a natural and clear way into your video controls. The example below is just food for thought about how you could offer different viewing options:

<Image title="Layout-options.gif" alt={600} src="https://files.readme.io/849cc52-Layout-options.gif">
  An example of different viewing options that could be offered to users
</Image>

Get creative and consider the following matrix of viewing options:

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Viewing mode
      </th>

      <th>
        Video cropped: OFF
      </th>

      <th>
        Video cropped: ON
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        1. Chat as tray
      </td>

      <td>
        **Chat tray with letterboxing**\
        Recommended as default view.
      </td>

      <td>
        **Chat tray with no letterboxing**
      </td>
    </tr>

    <tr>
      <td>
        2. Chat as overlay
      </td>

      <td>
        **Overlay + Tray**\
        Consider fading out chat above 50% in height. 

        Consider if a navigation sidebar can facilitate navigation of ancillary content (chat, stats...)
      </td>

      <td>
        **Overlay + No tray**\
        Keeping the chat as overlay but no side-menu.
      </td>
    </tr>

    <tr>
      <td>
        3. No chat
      </td>

      <td>
        **No chat + Tray**\
        Consider if a navigation sidebar can facilitate navigation of ancillary content (chat, stats...)
      </td>

      <td>
        **No chat + No Tray**\
        Taking advantage of the full width.
      </td>
    </tr>
  </tbody>
</Table>

## Widgets

Much like chat, widgets should complement the video content and not take away from it.\
Consider ways to overlay widgets in the least intrusive ways possible. If overlaying it on the video consider using a lower third placement. Consider also pop-in widgets on top of chat.
