---
title: Chat Message Mentions
excerpt: >-
  The Chat Message Mentions feature lets users tag specific profiles in a
  message.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Chat Message Mentions feature allows users to tag specific user profiles in chat messages.\
Mentions can be sent along with message creation and will be returned in the response of GET APIs.
There are two ways to mention users.

* **Explicit mentions**: Doesn’t requiring users to parse the message text manually for mentions.
* **Implicit mention**s: Implicit mentions are automatically extracted from message text by the backend using a specific pattern

Currently, we support explicit mentions only. Implicit mentions may be enabled in the future.