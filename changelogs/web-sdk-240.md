---
title: Web SDK 2.4.0
author: Justin Formentin
hidden: false
published_at: '2021-03-30T14:55:04.780Z'
---
## Release Notes

* Added support for Chat Reaction Icon customization
* Added addWidgetListener method
* Added removeWidgetListener method
* Added improvements for handling single tag widgets
* Fixed bug where multiple chat elements on the same page could sometimes received incorrect events
* Fixed bug where error was being logged when chat element loaded without stickers
* Fixed bug where error would occur when sending text message after sending image message
* Fixed bug where message-list-empty slot was not rendering correctly
* Changed default Cheer Meter UI to format very large images correctly
* Changed default widget UI to show vote percentages only after interaction