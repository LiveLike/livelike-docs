---
title: Program
excerpt: Representing your content inside of LiveLike
deprecated: false
hidden: false
metadata:
  robots: index
---
Programs are how you organize and represent your content inside of LiveLike. A program can represent a live stream, a blog post, a television episode, or any other unit of content you want to manage. All interactive widgets belong to a program. This ensures that polls, quizzes, alerts, and other widgets published to one program remain isolated from other programs.
Programs can also be linked to one or more leaderboards. Any rewards earned within a program automatically update all linked leaderboards.

## Scheduling Programs

Each program has scheduling fields to manage its lifecycle:

* Status → Can be future, live, or past.
* Scheduled At → Planned start time.
* Started At → The most recent time the program was started (null if never started).
* Stopped At → The most recent time the program was stopped (null if never stopped).

A program can be started and stopped multiple times. Live programs appear in the Live Now tab, upcoming programs in the Upcoming tab, and past programs in the History tab.

### Starting and Stopping Programs

* Starting a program flags it as live.
* Stopping a program signals it is no longer live.

The live status is primarily for organization within the CMS and for scheduling integrations. Integrations can listen to the program-status-updated pubsub event to trigger custom actions when a program starts or stops.
📘 Note: Live status does not affect widget publishing. Widgets can always be published to a program regardless of its live status.
Read more: Using Programs API

### Custom Identifiers

* Every program has a unique identifier assigned by LiveLike.
* You can also assign a custom ID per program.
* Custom IDs must be unique within your application.

Learn more: Custom Program IDs

### Moderation

* Profiles banned from a program cannot create or publish widgets in that program. See Program Bans.
* Widgets can be reported by users.
* Widget reports are visible in the CMS dashboard and via the List Widget Reports API.
