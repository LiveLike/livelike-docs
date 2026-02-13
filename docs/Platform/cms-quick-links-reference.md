---
title: CMS Quick Links Reference
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: ps-getting-started
      title: Getting Started
      type: basic
---
This document provides direct CMS links for all LiveLike resources. Replace `{{client_id}}` with your Application ID and resource-specific IDs (e.g., `{{program_id}}`, `{{widget_id}}`) with actual values.

<Callout icon="📘" theme="info">
  **Finding Your Client ID**

  Your Client ID (Application ID) can be found in the **Producer Suite** dashboard or provided by your LiveLike account representative.
</Callout>

***

## Producer Suite

The Producer Suite is your central hub for managing programs, widgets, chat, and all engagement features.

**Base URL:** `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}`

| Resource      | URL                                                                              |
| ------------- | -------------------------------------------------------------------------------- |
| **Dashboard** | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/dashboard` |

***

<Accordion title="Programs" icon="fa-info-circle">
  | Resource           | URL                                                                                              |
  | ------------------ | ------------------------------------------------------------------------------------------------ |
  | List all programs  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs`                  |
  | Live Now           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs?status=live`      |
  | Upcoming           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs?status=future`    |
  | History            | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs?status=past`      |
  | Moderation         | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reported-widgets`          |
  | Banned Users       | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/banned-users`              |
  | Filtered Widgets   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/widgets/filtered` |
  | View/Edit program  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}`   |
  | Create new program | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/create`           |
</Accordion>

<Accordion title="Widget" icon="fa-info-circle">
  | Resource     | URL                                                                                                                             |
  | ------------ | ------------------------------------------------------------------------------------------------------------------------------- |
  | Create       | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}`                                  |
  | Widgets      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}/widgets`                          |
  | Automated    | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?automating=True`                  |
  | Queue        | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?status=pending&ordering=recent`   |
  | Scheduled    | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?status=scheduled&ordering=recent` |
  | History      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?status=published&ordering=recent` |
  | Moderation   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?moderation=True`                  |
  | Banned Users | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}?banned_users=True`                |
</Accordion>

<Accordion title="Chat Rooms" icon="fa-info-circle">
  | Resource          | URL                                                                                                                |
  | ----------------- | ------------------------------------------------------------------------------------------------------------------ |
  | List all          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms`                                  |
  | Moderation        | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reported-chat-messages`                      |
  | Muted Users       | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/globally-muted-users`                        |
  | Banned Words      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/banned-words`                                |
  | Filtered Messages | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/filtered-messages`                           |
  | View/Edit room    | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}`                 |
  | Members           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}/members`         |
  | Room Moderation   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}/moderation`      |
  | Room Muted Users  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}/muted-users`     |
  | Pinned Messages   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}/pinned-messages` |
</Accordion>

<Accordion title="Comments (Comment Board)" icon="fa-info-circle">
  | Resource          | URL                                                                                                 |
  | ----------------- | --------------------------------------------------------------------------------------------------- |
  | Comment Board     | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/comment-board?is_linked=true` |
  | Reported Comments | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reported-comments`            |
  | Banned Users      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/globally-banned-user`         |
  | Filtered Comments | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/all-filtered-comments`        |
</Accordion>

<Accordion title="Moderation" icon="fa-info-circle">
  | Resource           | URL                                                                                                      |
  | ------------------ | -------------------------------------------------------------------------------------------------------- |
  | Widgets - Reported | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-reported-widgets`       |
  | Widgets - Filtered | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/filtered-section-widgets`          |
  | Chat Messages      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-reported-chat-messages` |
  | Comments           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-comments`               |
  | Image Origins      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-image-origins`          |
  | Banned Words       | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/banned-words`                      |
</Accordion>

<Accordion title="Asset Packs" icon="fa-info-circle">
  | Resource       | URL                                                                                   |
  | -------------- | ------------------------------------------------------------------------------------- |
  | Sticker Packs  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sticker-packs`  |
  | Reaction Packs | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reaction-packs` |
  | Flairs         | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/flair-list`     |
</Accordion>

<Accordion title="Media Library" icon="fa-info-circle">
  | Resource      | URL                                                                          |
  | ------------- | ---------------------------------------------------------------------------- |
  | Media Library | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/media` |
</Accordion>

***

## Loyalty & Rewards

<Accordion title="User Actions" icon="fa-info-circle">
  | Resource           | URL                                                                                             |
  | ------------------ | ----------------------------------------------------------------------------------------------- |
  | All Actions        | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=all`       |
  | Built-In           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=built-in`  |
  | Custom             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=custom`    |
  | Segment            | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=segment`   |
  | mParticle          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=mParticle` |
  | Create User Action | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions/create`           |
</Accordion>

<Accordion title="Rewards" icon="fa-info-circle">
  | Resource       | URL                                                                                                 |
  | -------------- | --------------------------------------------------------------------------------------------------- |
  | Reward Items   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-items`                 |
  | Reward Tables  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-tables`                |
  | Archived Items | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-items?status=archived` |
</Accordion>

<Accordion title="Leaderboards" icon="fa-info-circle">
  | Resource              | URL                                                                                                    |
  | --------------------- | ------------------------------------------------------------------------------------------------------ |
  | List all leaderboards | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards`                    |
  | View/Edit leaderboard | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards/{{leaderboard_id}}` |
</Accordion>

<Accordion title="Status Tiers" icon="fa-info-circle">
  | Resource          | URL                                                                                                   |
  | ----------------- | ----------------------------------------------------------------------------------------------------- |
  | Active            | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/tier-groups/?is_archived=false` |
  | Archived          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/tier-groups/?is_archived=true`  |
  | Create Tier Group | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/create-tier-group/`             |
</Accordion>

<Accordion title="Quests" icon="fa-info-circle">
  | Resource         | URL                                                                                           |
  | ---------------- | --------------------------------------------------------------------------------------------- |
  | Open             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests`                 |
  | Expired          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests?is_expired=true` |
  | Archived         | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests?is_active=false` |
  | View/Edit quest  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/{{quest_id}}`    |
  | Create new quest | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/create`          |
</Accordion>

<Accordion title="Streaks" icon="fa-info-circle">
  | Resource | URL                                                                                                    |
  | -------- | ------------------------------------------------------------------------------------------------------ |
  | Live     | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=live`     |
  | Upcoming | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=upcoming` |
  | Expired  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=expired`  |
  | Archived | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=archived` |
  | Draft    | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=draft`    |
</Accordion>

<Accordion title="Badges" icon="fa-info-circle">
  Badges tabs (Active, Archived) are JS-based and share the same URL. Badge creation and editing use modal dialogs on the list page.

  | Resource                   | URL                                                                           |
  | -------------------------- | ----------------------------------------------------------------------------- |
  | Badges (Active / Archived) | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/badges` |
</Accordion>

<Accordion title="NFTs" icon="fa-info-circle">
  | Resource    | URL                                                                         |
  | ----------- | --------------------------------------------------------------------------- |
  | Manage NFTs | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/nfts` |
</Accordion>

***

## Business Tools

<Accordion title="Sponsors" icon="fa-info-circle">
  | Resource          | URL                                                                             |
  | ----------------- | ------------------------------------------------------------------------------- |
  | List all sponsors | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sponsors` |
</Accordion>

<Accordion title="Integrations" icon="fa-info-circle">
  | Resource          | URL                                                                                 |
  | ----------------- | ----------------------------------------------------------------------------------- |
  | View integrations | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/integrations` |
</Accordion>

<Accordion title="Analytics" icon="fa-info-circle">
  | Resource            | URL                                                                                                                   |
  | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
  | Analytics Dashboard | `https://cf-blast.livelikecdn.com/analytics/visualization?organization={{organization_id}}&application={{client_id}}` |
</Accordion>

<Accordion title="LiveLike Genie (AI Assistant)" icon="fa-info-circle">
  | Resource   | URL                                                                          |
  | ---------- | ---------------------------------------------------------------------------- |
  | Open Genie | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/genie` |
</Accordion>

<Accordion title="Redemption Keys" icon="fa-info-circle">
  | Resource | URL                                                                                                    |
  | -------- | ------------------------------------------------------------------------------------------------------ |
  | Active   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys`                 |
  | Redeemed | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys?status=redeemed` |
  | Archived | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys?status=archived` |
</Accordion>

***

## User Management

<Accordion title="User Profiles & User Groups" icon="fa-info-circle">
  | Resource                | URL                                                                                                |
  | ----------------------- | -------------------------------------------------------------------------------------------------- |
  | User Profiles           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/user-profile`                |
  | User Groups             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups`              |
  | View/Edit profile group | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups/{{group_id}}` |
</Accordion>

<Accordion title="User Roles" icon="fa-info-circle">
  | Resource       | URL                                                                          |
  | -------------- | ---------------------------------------------------------------------------- |
  | List all roles | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/roles` |
</Accordion>

<Accordion title="Registered Links" icon="fa-info-circle">
  | Resource                  | URL                                                                                     |
  | ------------------------- | --------------------------------------------------------------------------------------- |
  | List all registered links | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/registered_links` |
</Accordion>

***

## Arcade CMS

The Arcade CMS is a separate portal for managing mini-games and interactive experiences.

**Base URL:** `https://arcade-cms.livelikecdn.com/application/{{client_id}}`

<Accordion title="Trivia" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                |
  | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/trivia`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/trivia/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Spin the Wheel" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                        |
  | --------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/spin-the-wheel`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/spin-the-wheel/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Guess the Word" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                |
  | --------- | ---------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/wordle`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/wordle/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Predictor" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                   |
  | --------- | ------------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/predictor`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/predictor/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Guess What" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                    |
  | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/guess-what`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/guess-what/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Skill Game" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                    |
  | --------- | -------------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/skill-game`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/skill-game/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Sweepstakes" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                     |
  | --------- | --------------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/sweepstakes`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/sweepstakes/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

<Accordion title="Scratch Card" icon="fa-info-circle">
  | Resource  | URL                                                                                                                                      |
  | --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
  | Game List | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/scratch-card`                                                        |
  | Edit Game | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/scratch-card/update?game_id={{game_id}}&instance_id={{instance_id}}` |
</Accordion>

## Arcade Game Preview

<Accordion title="Arcade Preview Links" icon="fa-info-circle">
  `https://arcade-web.livelikecdn.com/{{game-type}}.html?client_id={{client_id}}&game_id={{game_id}}&instance_id={{instance_id}}`
</Accordion>

<br />
