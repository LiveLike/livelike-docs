---
title: iOS SDK 2.79
author: jelzon monzon
hidden: false
published_at: '2023-11-07T15:38:10.385Z'
---
# What's New?

* [Chat] Adds ability to disable the image picker button in the ChatViewController
* ```
  let chatVC = ChatViewController()
  chatVC.supportImagePicker = false
  ```
* [Widget] Adds theme properties for vertical and horizontal offsets for the image of image poll, image quiz, and image predictions widgets

# Bugfixes

* [Chat] Fixes issue where user is unable to send a single message when using ChatViewController