---
title: iOS SDK 2.6 - Widget Triggers
author: Victor Matos
hidden: false
published_at: '2020-07-31T19:09:58.174Z'
---
In this iOS SDK release, we empowered developers with the ability to trigger widgets without using the CMS.

## Overview

We've allowed developers the ability to manually trigger widgets without the need to use the LiveLike CMS. This opens up the opportunity to deep link a particular LiveLike widget, and even embed a LiveLike widget on a webpage or app screen.

## 2.6.0 Release Notes

\*Integrators can now retrieve a widget and present it to a user at any point in time.

* Fixed a bug where the reaction panel would open even after the message is deleted from the CMS
* Fixed a bug where moving from one widget state to the next can cause a delay in the setting of the **widget.currentState** making it not a true representation of the state of the widget.