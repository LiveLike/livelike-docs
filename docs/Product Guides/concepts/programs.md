---
title: Programs
excerpt: Representing your content inside of LiveLike
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: custom-program-ids
      title: Custom Program IDs
    - type: basic
      slug: widgets
      title: Widgets
    - type: basic
      slug: leaderboards
      title: Leaderboards
---
Programs are how you organize and represent your content inside of LiveLike. A program can represent a live stream, a blog post, a television episode, or any other unit of content you might have.

Each interactive [widget](doc:widgets) is considered part of a program. Polls, quizzes, alerts, and any other widgets published to one program will not appear in another.

Programs can be linked with one or more [leaderboards](doc:leaderboards). [Rewards](doc:rewards) earned in the context of a program will automatically update all leaderboards linked to that program.

## Scheduling Programs

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a40f0c2-ProgramSchedulingDetail.png",
        "",
        "Live programs appear in the Live Now tab of the Programs section. Future programs will appear in the Upcoming tab, and past programs can be found in the History tab."
      ],
      "align": "center",
      "caption": "Live programs appear in the Live Now tab of the Programs section. Future programs will appear in the Upcoming tab, and past programs can be found in the History tab."
    }
  ]
}
[/block]


Each program has fields for scheduling information such as starting time and status. Those fields are:

- **Status**: can be one of future, live, or past.
- **Scheduled At**: when the program is planned to start.
- **Started At**: when the program was most recently started. Will be null if the program hasn't been started before.
- **Stopped At**: when the program was most recently stopped. Will be null if the program hasn't been stopped before.

A program can be started and stopped multiple times.

## Starting and Stopping Programs

Starting a program flags it as live, and stopping a program signals that it is no longer live. The live status is purely for organizational purposes inside of the CMS and for adding scheduling hook points to integration. Integrations can listen for the `program-status-updated` pubsub event to implement their own custom handlers for a program starting and stopping.

> 📘 Live status does not affect widget publishing
> 
> Widgets can always be published to programs whether or not they are live. Live status is used by the CMS for organization and navigational purposes, but no business logic is enforced by LiveLike related to the live status of a program.

## Custom Identifiers

Each program as a unique identifier assigned by LiveLike, but you can also supply your own additional custom ID per program. A program's custom ID must be unique inside your application. For more details about using custom IDs, check out [Custom Program IDs](doc:custom-program-ids).

## Moderation

A profile that has been banned from a program may not create or publish widgets inside of that program. You can read more about [Program Bans](ref:program-bans) in the API reference.

Widgets can be reported by users. Widget reports from users appear in the dashboard and also in the [List widget reports](ref:list-widget-reports) API.