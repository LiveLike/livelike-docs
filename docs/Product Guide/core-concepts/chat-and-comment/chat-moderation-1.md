---
title: Chat Moderation
deprecated: false
hidden: false
metadata:
  robots: index
---
A strong moderation toolkit is essential for building a safe and engaging community.
LiveLike provides flexible moderation options that can be tailored to your app’s content policies and moderation workflows.

## Automatic Filtering

Chat messages can be filtered before reaching the community:

* **Keyword-driven filtering**: Messages containing words from a customizable bad-word list can be automatically flagged or hidden. Filtering can be strict (whole-word matching) or lenient (detecting partially obfuscated words).
* **AI-driven filtering**: Messages can be evaluated by AI models that identify objectionable or harmful content in real time.

<Callout icon="📘" theme="info">
  By default, the SDK hides filtered messages from everyone except the sender.
</Callout>

***

## Moderator Tools

Moderators get additional capabilities for active community management:

* **Delete messages**: Remove inappropriate or harmful messages directly from the chat.
* **User reports**: Community members can report objectionable content. Moderators can review these reports and take action.
* **User blocking**: Users can block others to prevent unwanted interactions. [Read more about Blocking](doc:blocking-profiles).
* **User muting**: Moderators can mute a user. Once muted, that user can no longer send messages in the chatroom.

***

## Learn More

Moderation can also be managed through the **Chat Moderation Tool in CMS**, which provides a dashboard view for real-time monitoring and control.
