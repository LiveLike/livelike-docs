---
title: Widgets
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Widgets | Fan Engagement Tools | LiveLike Developer Hub
  description: >-
    This document provides an overview of widgets, including different
    presentation modes and types of interactive elements such as polls, quizzes,
    and predictions. It also explains the options for widget interactivity and
    customization of widget UI.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: custom-themes
      title: Custom Themes
---
![](https://files.readme.io/c74645a-banner_widgets.jpg "banner_widgets.jpg")

The various interactive elements that are delivered to audiences to engage with are called widgets. The library of widgets is always expanding and features things like polls, quizzes, and predictions. Widgets can be created and published manually by producers using the [Producer Suite](doc:ps-getting-started), and can also be automated through the [REST API](doc:rest-api-getting-started).

Every widget is created as part of a <<glossary:Program>>. A program associates a sequence of widgets with some content. Every program has a Program ID that uniquely identifies the program within an application. Programs are also how content is managed inside of the Producer Suite and include metadata like scheduling information that helps producers keep their dashboards organized.

# Presentation Modes

The different ways Widgets are displayed in your application.

## Popup Widgets

Popup widgets are shown one at a time. Users have a limited time to engage with each widget before it goes away to make room for the next one. Some use cases for popup widgets include:

- Crowd polls
- In-play prediction games
- Trivia games
- Limited-time offers

Click the links below learn more about how to add Popup Widgets to your application:  
[iOS](doc:widget-view-controller)  
[Android](doc:widget-pop-up-view)  
[Web](https://docs.livelike.com/docs/web-widget-modes#popup-mode)

## Timeline Widets

Timeline widgets are shown all at once. Users can browse through them and interact with past widgets. Some use cases for timeline widgets include:

- Live blogging
- Match commentary
- Pick 'em games

Click the links below learn more about how to add Timeline Widgets to your application:  
[iOS](doc:interactive-widget-timeline-view-controller)  
[Android](https://docs.livelike.com/docs/widget-timeline)  
[Web](https://docs.livelike.com/docs/web-widget-modes#timeline-mode)

## Embedded Widgets

Individual widgets can be embedded on web pages. Basic embed codes can be copied from inside of the Producer Suite, and you can also generate your own embed codes inside your own templates. Browse the [Web Embeds](doc:web-embeds) documentation to learn more.

# Widget Interactivity

You can set the widget expiry UTC Time. Widget will no longer be interactive after the selected date and time.

![](https://files.readme.io/da623ec-Interactivity_Expiry.png "Interactivity Expiry.png")

# Widget Library

The variety of Widgets that you can use to Engage your users.

## Polls

Get your audience’s opinion. Ask questions and see results update live as votes are cast.

Polls ask audiences questions that don’t necessarily have any right answers. The results update live **so** everyone voting feels like they are part of the crowd.

- Audience opinion
- Gather feedback
- Results revealed immediately and update live

You can create text polls or image polls. Image polls allow you to illustrate each answer with an image such as a player photo.

![](https://files.readme.io/83651e6-image_poll_5.gif "image_poll_5.gif")

## Image Slider

An image slider is essentially a poll to which audience respond using using a scale. It allows audience to give their opinion using a more visual, fun and emotional way.

Add between 1 to 5 images to illustrate different steps in the scale. If have a a single image, the image will scale up as you move form left to right.

![](https://files.readme.io/4d2f0e3-image_poll_4.gif "image_poll_4.gif")

## Trivia / Quiz

Challenge your audience’s knowledge.  
Quizzes ask audiences questions that have at least one correct answer. 

- Audience competition
- Results revealed when time expires

Gamification options: Everybody who answers collects points, and correct answers can earn higher points.

![](https://files.readme.io/3a4e3e0-image_poll_6.gif "image_poll_6.gif")

## Predictions

Keep your audience’s attention. Ask them to predict the future and creating a reason for fans to stick around for the big reveal.

Predictions are a two-step interaction. In the first step, the prediction, the producer asks the audience a question for which the answer is not yet known and provides some answers to choose from. In the second step, the producer follows-up to reveal which answer turned out to be correct. 

- Audience suspense & appointment dynamics
  - Short term: Guess the penalty outcome?
  - Medium term: Which team will score more rushing yard this quarter?
  - Long term: Who will win the match?
- Results revealed when producer is ready

![](https://files.readme.io/95fa43e-image_poll_7.gif "image_poll_7.gif")

## Cheer Meter

Let your audience battle out on topics such as which team they support, or show what mood they're in.

You can provide up to two options in the form of a text and image. Users can tap as quickly as possible for any option to show their support. Users receive feedback to how many times they tapped.

In the default scenario, the most popular option is deemed the winner.

![](https://files.readme.io/5a84146-image_poll_9.gif "image_poll_9.gif")

## Alerts

Inform your audience. Broadcast breaking headlines, GIFs, special offers, or provide a commentary, at just the right time.

Alerts are a versatile widget. Use them to broadcast text, media, or a combination of both. Additionally, links can be attached for use as sponsorship, media or advertisement destinations. The link can also be as a point of integration for other apps and websites such as a betting app of a partner.

- Headlines
- Graphics
- Advertisements
- Deep links
- Content suggestion at the end of a stream

![](https://files.readme.io/04ad2e4-image_poll_11-min.gif "image_poll_11-min.gif")

## Ask

Ask your audience. Collect their replies, and feature the best ones.

You can gather open-ended feedback, or compile a list of questions from the crowd to ask to on-air talent. Allow everyone watching to share their input, and maybe see their content featured in the experience.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/afc7afd-ask-widget--new.gif",
        "ask-widget--new.gif",
        1074
      ],
      "align": "center",
      "sizing": "smart"
    }
  ]
}
[/block]

## Number Prediction

Allow your audience to make predictions as numbers so that you can ask about things like sports scores, player performance, number of seconds in a national anthem, etc.

![](https://files.readme.io/4b3ff08-Number-Prediction.gif "Number-Prediction.gif")

## Social Embeds

Embed content from Twitter, Facebook, or any other provider that supports [oEmbed](https://oembed.com/).

# Widget UI and Styling

The different options of Widget UI to best fit your application.

## Stock UI

The Engagement SDK has bundled UI for Widgets. These are designed by LiveLike to be user-friendly, fun and engaging, includes analytics, continuously improved and maintained.

We understand that every app is different and our designs style may not fit into yours. For these cases, you can either use the Theme system to alter the Stock UI to generally match your app design or you can design and develop your own Custom UI to work with the Engagement ecosystem.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/63e0d43-50b616a-stock_ui.gif",
        "50b616a-stock_ui.gif",
        375
      ],
      "align": "center",
      "caption": "The Stock UI for Poll Widget"
    }
  ]
}
[/block]

## Themed Stock UI

The Theme system allows you to alter the look of the Engagement SDK’s Stock Widget UI. This includes common UI properties such as background colors and border colors, corner radii, and text size and fonts. Those customizations are saved in a standard format and can be reused across platforms.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/65113ef-1a6f870-themed_stock_ui.gif",
        "1a6f870-themed_stock_ui.gif",
        375
      ],
      "align": "center",
      "caption": "The Stock UI for Poll Widget Themed to a green app style."
    }
  ]
}
[/block]

Learn more about [Custom Themes](doc:custom-themes) here!

Theme options are inherently limited - if you need more control of the Widgets UI we recommend that you go the Custom UI route.

## Custom UI

Although the EngagementSDK offers high-fidelity widget UI which provide engaging experiences for your users, you may want to design and develop your own UI to match your applications particular use-case or aesthetic.  
We can guarantee that any changes to the Stock UI will not affect any Custom UI that you have built. Any changes to the Widget Models are backwards compatible.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/307f534-eaab79c-cust_ui.gif",
        "eaab79c-cust_ui.gif",
        375
      ],
      "align": "center",
      "caption": "An alternative UI design which was custom built to fit into a specific app style. \n\nThe placement of the percentage and option text animation are examples of design changes that aren't feasible with the Theme system."
    }
  ]
}
[/block]

Learn more about [Building Custom Widget UI](doc:custom-widget-ui) here!