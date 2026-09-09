---
title: AI content Moderation
excerpt: >-
  AI moderation adds an automatic check on top of the standard profanity filter,
  so harmful messages and comments are hidden without a moderator having to
  catch them first.
deprecated: false
hidden: false
metadata:
  robots: index
---
## How it works

1. A user posts a chat message or a comment.
2. The profanity filter runs first. Anything matching your blocklist is masked immediately.
3. Everything that passes the blocklist is then reviewed by the AI model. If it judges the<br />content harmful, the  whole content is masked and replaced with `***`.

The AI review runs in the background, so a flagged message is hidden a moment after it is
posted rather than being blocked before it appears.

## Turning it on

AI moderation can be enabled in the cms per-chat-room and per-comment-board.

Open the chat room or comment board in CMS ->  Create or Edit -> Set **Content filter** to<br />`Profanity and AI content filtering`.&#x20;
