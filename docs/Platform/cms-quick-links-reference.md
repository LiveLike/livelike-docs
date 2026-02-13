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

> 📘 **Finding Your Client ID**
> Your Client ID (Application ID) can be found in **Organization Settings** within the Producer Suite or provided by your LiveLike account representative.

---

## Producer Suite

The Producer Suite is your central hub for managing programs, widgets, and chat.

| Resource | Action | URL |
|----------|--------|-----|
| **Dashboard** | View | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/dashboard` |
| **Organization Settings** | Manage | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/settings` |

### Programs

| Action | URL |
|--------|-----|
| List all programs | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs` |
| View/Edit program | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}` |
| Create new program | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/new` |

### Widgets

| Action | URL |
|--------|-----|
| Widget Console (by program) | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}/widgets` |
| View widget details | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/widgets/{{widget_id}}` |

### Chat Rooms

| Action | URL |
|--------|-----|
| List all chat rooms | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms` |
| View/Edit chat room | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/chat-rooms/{{chat_room_id}}` |
| Moderation panel | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/moderation` |

---

## Engagement & Gamification

### Rewards

| Resource | Action | URL |
|----------|--------|-----|
| **Reward Items** | List all | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/rewards/items` |
| **Reward Items** | View/Edit | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/rewards/items/{{reward_item_id}}` |
| **Reward Actions** | List all | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/rewards/actions` |
| **Reward Tables** | List all | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/rewards/tables` |
| **Reward Tables** | View/Edit | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/rewards/tables/{{table_id}}` |

### Leaderboards

| Action | URL |
|--------|-----|
| List all leaderboards | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards` |
| View/Edit leaderboard | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards/{{leaderboard_id}}` |
| Create new leaderboard | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/leaderboards/new` |

### Quests

| Action | URL |
|--------|-----|
| List all quests | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests` |
| View/Edit quest | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/{{quest_id}}` |
| Create new quest | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/quests/new` |

### Badges

| Action | URL |
|--------|-----|
| List all badges | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/badges` |
| View/Edit badge | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/badges/{{badge_id}}` |
| Create new badge | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/badges/new` |

### Streaks

| Action | URL |
|--------|-----|
| List all streaks | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks` |
| View/Edit streak | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks/{{streak_id}}` |
| Create new streak | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/streaks/new` |

### Sponsors

| Action | URL |
|--------|-----|
| List all sponsors | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sponsors` |
| View/Edit sponsor | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sponsors/{{sponsor_id}}` |
| Create new sponsor | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/sponsors/new` |

---

## User Management

### Profile Groups

| Action | URL |
|--------|-----|
| List all profile groups | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups` |
| View/Edit profile group | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/profile-groups/{{group_id}}` |

### Registered Links

| Action | URL |
|--------|-----|
| List all registered links | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/registered-links` |
| View/Edit registered link | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/registered-links/{{link_id}}` |

---

## Arcade CMS

The Arcade CMS is a separate portal for managing mini-games and interactive experiences.

**Base URL:** `https://arcade-cms.livelikecdn.com/application/{{client_id}}`

| Game Type | List All | Edit Game |
|-----------|----------|-----------|
| **Trivia** | `/games/trivia` | `/games/trivia/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Spin the Wheel** | `/games/spin-the-wheel` | `/games/spin-the-wheel/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Guess the Word** | `/games/wordle` | `/games/wordle/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Predictor** | `/games/predictor` | `/games/predictor/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Guess What** | `/games/guess-what` | `/games/guess-what/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Skill Game** | `/games/skill-game` | `/games/skill-game/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Sweepstakes** | `/games/sweepstakes` | `/games/sweepstakes/update?game_id={{game_id}}&instance_id={{instance_id}}` |
| **Scratch Card** | `/games/scratch-card` | `/games/scratch-card/update?game_id={{game_id}}&instance_id={{instance_id}}` |

### Arcade Preview Links

To preview arcade games, use the following URL pattern:
https://arcade-web.livelikecdn.com/{{game-type}}.html?client_id={{client_id}}&game_id={{game_id}}&instance_id={{instance_id}}


**Example (Guess the Word):**
https://arcade-web.livelikecdn.com/guess-the-word.html?client_id={{client_id}}&game_id={{game_id}}&instance_id={{instance_id}}


---

## Analytics

| Resource | URL |
|----------|-----|
| Analytics Dashboard | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/analytics` |
| Program Analytics | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}/programs/{{program_id}}/analytics` |

---

## URL Pattern Reference

For developers building integrations or custom tooling, here are the base URL patterns:

| Environment | Base URL |
|-------------|----------|
| Producer Suite | `https://cf-blast.livelikecdn.com/producer/applications/{{client_id}}` |
| Arcade CMS | `https://arcade-cms.livelikecdn.com/application/{{client_id}}` |
| Arcade Preview | `https://arcade-web.livelikecdn.com/` |

---

## Related Resources

- [Producer Suite Getting Started](https://docs.livelike.com/docs/ps-getting-started)
- [REST API Getting Started](https://docs.livelike.com/docs/rest-api-getting-started)
- [API Reference](https://docs.livelike.com/reference)

---

> 💡 **Tip:** Bookmark this page for quick access to any CMS resource. You can also use browser search (Ctrl/Cmd + F) to quickly find the link you need.