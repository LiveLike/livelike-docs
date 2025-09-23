---
title: Stickers
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Stickers | Sticker Packs & Custom Stickers | LiveLike
  description: >-
    Stickers are images or animations that can be used in a chat room. They can
    be customized to match an app's look and feel.
  robots: index
next:
  description: ''
---
![1120](https://files.readme.io/6737954-0347be3-sticker_kb.gif "0347be3-sticker_kb.gif")

Stickers are images or animations that can be used inside of [chat messages](doc:chat). They can be customized to match an app's look and feel.

## Sticker Packs

Stickers are collected into _packs_ that can usually have a shared theme or art style. Usually packs are focused on particular concepts such as:

* Players
* Teams
* Leagues
* Crowd Reactions
* Personalities

<Image align="center" alt={563} border={false} caption="Each pack has its own icon that will help people find it in their soft keyboards." title="sticker kb behavior.gif" src="https://files.readme.io/5239f1d-sticker_kb_behavior.gif" width="auto" />

Many packs can be set up for an app, and then chats in that app can be configured individually to use different combinations of packs, or they can all share the same packs.

One chat can use many different packs, and different chats can use different combinations of available packs.

## Custom Stickers

Custom stickers can be created by your own team, following the [Chat Asset Guidelines](doc:chat-sticker-guidelines).

## Sponsorship

Custom stickers are also opportunities for brand partnerships and sponsorships. LiveLike can deliver [analytics and reports](doc:analytics-overview) that provide insights into when and how users interact with stickers.

## Exclusive Stickers

Exclusive stickers unlock a new layer of personalization and recognition inside community chats. Unlike standard packs, exclusive packs are only available to specific profiles — helping fans feel rewarded and distinguished, while also opening up new monetization and engagement opportunities.

<Callout icon="📘" theme="info">
   Exclusive packs are tied to profiles only. Access is managed at the profile level, and only those profiles granted access will see or use them inside chat. 
</Callout>

#### Sample Use Cases


* In-app purchases for fans who love collecting
* Team-branded packs available only to official fan communities (via individual profile assignment)
* Collectible packs redeemable through a Rewards Store
* Loyalty programs (e.g., Gold-tier members unlocking exclusive packs)

#### How It Works

* Access to exclusive sticker packs can be granted, revoked, or automated through purchases, loyalty tiers, or rewards.
* Fans will only see packs they own, ensuring clutter-free and personalized chat experiences.

#### APIs – Integrator Experience


* Grant Access to a Sticker Pack
  `POST /api/v1/profiles/{profile_uuid}/sticker-packs/`
  Grants access to an exclusive sticker pack for the specified profile.
  ```
  {
      "sticker_pack_id": "6e654321-abcd-4def-9012-9876543210fe"
  }
  ```
* List Sticker Packs Owned by a Profile
  `GET /api/v1/profiles/{profile_uuid}/sticker-packs/`
* Revoke Access to a Sticker Pack
  `DELETE /api/v1/profiles/{profile_uuid}/sticker-packs/{sticker_pack_id}/`

Integrators don’t need to manage exclusivity flags or backend models directly — simply use the APIs above to control which profiles have access.

<br />
