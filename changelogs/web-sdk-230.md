---
title: Web SDK 2.3.0
author: Justin Formentin
hidden: false
published_at: '2021-02-17T05:54:56.132Z'
---
## Release Notes

* Added support for using single widget HTML tags
* Added and updated widget tracking events and added associated program id to tracking properties
* Fixed bug related to widget duplication and event listener handling
* Fixed bug with vote count updating
* Deprecated langcode attribute from chat and widgets. Built-in lang attribute is used now
* Added Widget Interacted event in Alert widgets
* Bug fix in default slider widget with no timer not sending vote
* Fixed bug where multiple widgets elements with same program id in a webpage were not loading widgets
* Fixed bug of Widget Dismissed event not firing for finished/expired widgets