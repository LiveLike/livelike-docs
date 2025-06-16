---
title: Session Management
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Session Management | Android SDK | LiveLike Developer Hub
  description: >-
    A Content Session represents a user's subscription to a particular program.
    Learn more about Android SDK Session Management.
  robots: index
next:
  description: ''
---
[block:api-header]
{
  "title": "Start a Content Session"
}
[/block]
A Content Session represents a user's subscription to a particular program (typically a live, linear TV show, game or episode). To start a Content Session you will need a **Program ID**. Integrating teams are expected to create programs within the LiveLike system, either through the API or through the Producer Suite. The team should then copy the **Program ID**s into the relevant media metadata in their own systems, so that content sessions can be started along with media playback.

** Starting a Session **
[block:code]
{
  "codes": [
    {
      "code": "val session = engagementSDK.createContentSession(\"<program-id >\")\nwidget_view.setSession(session)\nchat_view.setSession(session.chatSession)",
      "language": "kotlin"
    },
    {
      "code": "ContentSession session = engagementSDK.createContentSession(\"<program-id>\");\nWidgetView widgetView = findViewById(R.id.widgetView);\nwidgetView.setSession(session);\nChatView chatView = findViewById(R.id.chatView);\nchatView.setSession(session);",
      "language": "java"
    }
  ]
}
[/block]
** Recommendations **

It is recommended to keep the session object separated from the activity lifecycle. If your session is destroyed (eg: Orientation change) the Widget and Chat state will be lost and the services disconnected.

If you are using a ViewModel it is a good practice to create the Content Session here.
[block:api-header]
{
  "title": "Pause a Content Session"
}
[/block]
Content Sessions can be **paused** to temporarily ignore all incoming Widgets and Chat messages until **resumed**. This can be useful if you need to display an advertisement without overlay from the Engagement SDK, as an example.
[block:callout]
{
  "type": "info",
  "title": "Removes all widgets on screen",
  "body": "When you pause or close a Content Session all widgets on screen will be removed, even if the user was interacting."
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "//Pause\nsession.pause()\n\n//Resume\nsession.resume()",
      "language": "kotlin"
    },
    {
      "code": "//Pause\nsession.pause();\n\n//Resume\nsession.resume();",
      "language": "java"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Close a Content Session"
}
[/block]
When the user returns to your application's home page and away from your live video screen you will want to **close** the ContentSession. Closing a session will disconnect from Widgets and Chat and release all the related resources.
**NOTE**: Once the session is closed, you cannot use the same session object again.
[block:code]
{
  "codes": [
    {
      "code": "session.close()",
      "language": "kotlin"
    },
    {
      "code": "session.close();",
      "language": "java"
    }
  ]
}
[/block]