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
4. Flagged content is listed in the CMS under **Filtered Messages** (chat) and **Filtered<br />Comments** for human review.

The AI review runs in the background, so a flagged message is hidden a moment after it is
posted rather than being blocked before it appears.

## Turning it on

AI moderation can be enabled in the cms per-chat-room and per-comment-board.

Open the chat room or comment board in CMS ->  Create or Edit -> Set **Content filter** to<br />`Profanity and AI content filtering`.&#x20;

## The default AI model

By default, AI moderation uses a **multilingual toxicity model**. It flags toxic and abusive<br />language and works across a wide range of languages out of the box, you do not need to<br />configure anything per language.

The same default model applies to both chat messages and comments.

## The default sensitivity threshold

Every AI decision comes with a confidence score. The default threshold is **0.99**. Content is only hidden when the model is **at least 99% confident** that it is harmful.

- A **lower** threshold makes moderation **stricter**: more content is caught, but more<br />acceptable content may be hidden by mistake.
- A **higher** threshold makes moderation **more lenient**: fewer false positives, but some<br />harmful content may get through.

The same default model applies to both chat messages and comments.

## Customising the model and threshold

Both the model and the sensitivity threshold can be tailored to your application. Chat and
comments are configured separately, so you can run stricter moderation on one than the other.

Available options include:

- **Multilingual toxicity**: general toxic and abusive language across many languages<br />(the default).
- **Detailed harm categories** — separates toxicity into categories such as threats, insults,
  identity-based hate, obscenity and sexually explicit content, with a **separate threshold per
  category**. This lets you be strict on threats and hate speech while staying more relaxed on
  mild insults.
- **Sentiment**: flags strongly negative content rather than toxicity, useful for<br />brand-sensitive or family-friendly environments.

**To change the model or the thresholds for your application, contact the LiveLike support**<br />**team.** Let us know which content type (chat or comments) you want to adjust and how strict you<br />would like it to be, and we will configure it for you.

## Good to know

- AI moderation works alongside your profanity blocklist, it does not replace it. Content<br />masked by the blocklist stays masked and never reaches to AI moderation.
- Comments are re-checked if the author edits them.
- Reviewing flagged content does not retrain the model. If you see recurring mistakes, share<br />examples with LiveLike support and we can adjust the thresholds.
- One AI moderation configuration is active per application per content type, so behaviour is
  consistent across all your rooms and boards using the AI filter.
