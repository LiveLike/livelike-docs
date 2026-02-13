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

> **Finding Your Client ID**
>
> Your Client ID (Application ID) can be found in the **Producer Suite** dashboard or provided by your LiveLike account representative.

***

## Producer Suite

The Producer Suite is your central hub for managing programs, widgets, chat, and all engagement features.

**Base URL:** `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}`

| Resource      | URL                                                                              |
| ------------- | -------------------------------------------------------------------------------- |
| **Dashboard** | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/dashboard` |

***

### Programs

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

#### Widget (Program Detail)

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

### Chat Rooms

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

### Comments (Comment Board)

| Resource          | URL                                                                                                 |
| ----------------- | --------------------------------------------------------------------------------------------------- |
| Comment Board     | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/comment-board?is_linked=true` |
| Reported Comments | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reported-comments`            |
| Banned Users      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/globally-banned-user`         |
| Filtered Comments | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/all-filtered-comments`        |

### Moderation

| Resource           | URL                                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------------- |
| Widgets - Reported | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-reported-widgets`       |
| Widgets - Filtered | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/filtered-section-widgets`          |
| Chat Messages      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-reported-chat-messages` |
| Comments           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-comments`               |
| Image Origins      | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation-image-origins`          |
| Banned Words       | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/banned-words`                      |

### Asset Packs

| Resource       | URL                                                                                   |
| -------------- | ------------------------------------------------------------------------------------- |
| Sticker Packs  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sticker-packs`  |
| Reaction Packs | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reaction-packs` |
| Flairs         | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/flair-list`     |

### Media Library

| Resource      | URL                                                                          |
| ------------- | ---------------------------------------------------------------------------- |
| Media Library | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/media` |

***

## Loyalty & Rewards

### User Actions

| Resource           | URL                                                                                             |
| ------------------ | ----------------------------------------------------------------------------------------------- |
| All Actions        | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=all`       |
| Built-In           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=built-in`  |
| Custom             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=custom`    |
| Segment            | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=segment`   |
| mParticle          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions?search=mParticle` |
| Create User Action | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/actions/create`           |

### Rewards

| Resource       | URL                                                                                                 |
| -------------- | --------------------------------------------------------------------------------------------------- |
| Reward Items   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-items`                 |
| Reward Tables  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-tables`                |
| Archived Items | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/reward-items?status=archived` |

### Leaderboards

| Resource              | URL                                                                                                    |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| List all leaderboards | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards`                    |
| View/Edit leaderboard | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards/{{leaderboard_id}}` |

### Status Tiers

| Resource          | URL                                                                                                   |
| ----------------- | ----------------------------------------------------------------------------------------------------- |
| Active            | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/tier-groups/?is_archived=false` |
| Archived          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/tier-groups/?is_archived=true`  |
| Create Tier Group | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/create-tier-group/`             |

### Quests

| Resource         | URL                                                                                           |
| ---------------- | --------------------------------------------------------------------------------------------- |
| Open             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests`                 |
| Expired          | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests?is_expired=true` |
| Archived         | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests?is_active=false` |
| View/Edit quest  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/{{quest_id}}`    |
| Create new quest | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/create`          |

### Streaks

| Resource | URL                                                                                                    |
| -------- | ------------------------------------------------------------------------------------------------------ |
| Live     | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=live`     |
| Upcoming | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=upcoming` |
| Expired  | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=expired`  |
| Archived | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=archived` |
| Draft    | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks?search=&status=draft`    |

### Badges

Badges tabs (Active, Archived) are JS-based and share the same URL. Badge creation and editing use modal dialogs on the list page.

| Resource                   | URL                                                                           |
| -------------------------- | ----------------------------------------------------------------------------- |
| Badges (Active / Archived) | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/badges` |

### NFTs

| Resource    | URL                                                                         |
| ----------- | --------------------------------------------------------------------------- |
| Manage NFTs | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/nfts` |

***

## Business Tools

### Sponsors

| Resource          | URL                                                                             |
| ----------------- | ------------------------------------------------------------------------------- |
| List all sponsors | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sponsors` |

### Integrations

| Resource          | URL                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------- |
| View integrations | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/integrations` |

### Analytics

| Resource            | URL                                                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Analytics Dashboard | `https://cf-blast.livelikecdn.com/analytics/visualization?organization={{organization_id}}&application={{client_id}}` |

### LiveLike Genie (AI Assistant)

| Resource   | URL                                                                          |
| ---------- | ---------------------------------------------------------------------------- |
| Open Genie | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/genie` |

### Redemption Keys

| Resource | URL                                                                                                    |
| -------- | ------------------------------------------------------------------------------------------------------ |
| Active   | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys`                 |
| Redeemed | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys?status=redeemed` |
| Archived | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/redemption_keys?status=archived` |

***

## User Management

### User Profiles & User Groups

| Resource                | URL                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------- |
| User Profiles           | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/user-profile`                |
| User Groups             | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups`              |
| View/Edit profile group | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups/{{group_id}}` |

### User Roles

| Resource       | URL                                                                          |
| -------------- | ---------------------------------------------------------------------------- |
| List all roles | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/roles` |

### Registered Links

| Resource                  | URL                                                                                     |
| ------------------------- | --------------------------------------------------------------------------------------- |
| List all registered links | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/registered_links` |

***

## Arcade CMS

The Arcade CMS is a separate portal for managing mini-games and interactive experiences.

**Base URL:** `https://arcade-cms.livelikecdn.com/application/{{client_id}}`

| Game Type          | List All                                                                            | Edit Game                                                                                                                                  |
| ------------------ | ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Trivia**         | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/trivia`         | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/trivia/update?game_id={{game_id}}&instance_id={{instance_id}}`         |
| **Spin the Wheel** | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/spin-the-wheel` | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/spin-the-wheel/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Guess the Word** | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/wordle`         | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/wordle/update?game_id={{game_id}}&instance_id={{instance_id}}`         |
| **Predictor**      | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/predictor`      | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/predictor/update?game_id={{game_id}}&instance_id={{instance_id}}`      |
| **Guess What**     | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/guess-what`     | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/guess-what/update?game_id={{game_id}}&instance_id={{instance_id}}`     |
| **Skill Game**     | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/skill-game`     | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/skill-game/update?game_id={{game_id}}&instance_id={{instance_id}}`     |
| **Sweepstakes**    | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/sweepstakes`    | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/sweepstakes/update?game_id={{game_id}}&instance_id={{instance_id}}`    |
| **Scratch Card**   | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/scratch-card`   | `https://arcade-cms.livelikecdn.com/application/{{client_id}}/games/scratch-card/update?game_id={{game_id}}&instance_id={{instance_id}}`   |

### Arcade Preview Links

`https://arcade-web.livelikecdn.com/{{game-type}}.html?client_id={{client_id}}&game_id={{game_id}}&instance_id={{instance_id}}`

***
