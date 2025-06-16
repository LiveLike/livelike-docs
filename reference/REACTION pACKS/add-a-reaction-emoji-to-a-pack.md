---
title: Add a Reaction emoji to a pack
excerpt: ''
api:
  file: engagement-suite.json
  operationId: add-a-reaction-emoji-to-a-pack
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 Support for system emojis isn't available in current SDK versions and will be incorporated in future releases.

> 📘 The default behaviour for this endpoint expects a mandatory file field value to store as an image for the reaction. If the query parameter emoji is set to true, at least one of the fields (file or emoji_unicode) can be passed and that will be handled accordingly to create a new reaction emoji.