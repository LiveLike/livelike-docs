---
title: Webhook Events Payload
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This document details the webhook events sent by our system, including their payload structures and descriptions of each field.

## `reward-table-rewards-awarded`

**Payload Structure:**

```json
{
    "id": "76f574bd-c986-40a2-84fe-5e551fdfe375",
    "event": "reward-table-rewards-awarded",
    "data": {
        "reward_transaction_id": "reward-transaction-id",
        "reward_item_id": "reward-item-uuid",
        "reward_item_amount": 100,
        "reward_item_balance": 1000,
        "reward_action_id": "action-uuid",
        "reward_action_key": "play-game",
        "reward_table_id": "table-uuid",
        "client_id": "client-id",
        "profile_id": "profile-uuid",
        "profile_custom_id": "custom-id"
    },
    "created_at": "2024-09-02T12:34:56Z"
}
```

**Field Descriptions:**

| Field                   | Type   | Description                                        |
| ----------------------- | ------ | -------------------------------------------------- |
| `id`                    | string | Unique identifier for the webhook event.           |
| `event`                 | string | The event type.                                    |
| `reward_transaction_id` | string | Unique ID of the reward transaction.               |
| `reward_item_id`        | string | Unique ID of the reward item.                      |
| `reward_item_amount`    | number | Amount of the reward item awarded.                 |
| `reward_item_balance`   | number | Remaining balance of the reward item.              |
| `reward_action_id`      | string | Unique ID of the action that triggered the reward. |
| `reward_action_key`     | string | Key of the action that triggered the reward.       |
| `reward_table_id`       | string | ID of the reward table.                            |
| `client_id`             | string | ID of the client associated with the reward.       |
| `profile_id`            | string | ID of the profile receiving the reward.            |
| `profile_custom_id`     | string | Custom identifier for the profile.                 |
| `created_at`            | string | Timestamp when the event was created.              |

<br />

## `badge-awarded`

**Payload Structure:**

```json
{
    "id": "76f574bd-c986-40a2-84fe-5e551fdfe375",
    "event": "badge-awarded",
    "data": {
        "badge_id": "badge-id",
        "earned_badge_id": "earned_badge_id",
        "badge_title": "Badge Title",
        "description": "Badge Description",
        "reward_item_id": "reward-item-id",
        "reward_item_name": "Reward Item Name",
        "reward_item_threshold": 10,
        "image_url": "https://example.com/image.png",
        "client_id": "client-id",
        "profile_id": "profile-uuid",
        "profile_custom_id": "custom-id"
    },
    "created_at": "2024-09-02T12:34:56Z"
}
```

**Field Descriptions:**

| Field                   | Type   | Description                                      |
| ----------------------- | ------ | ------------------------------------------------ |
| `id`                    | string | Unique identifier for the webhook event.         |
| `event`                 | string | The event type.                                  |
| `badge_id`              | string | Unique ID of the badge.                          |
| `earned_badge_id`       | string | ID of the earned badge instance.                 |
| `badge_title`           | string | Title of the badge.                              |
| `description`           | string | Description of the badge.                        |
| `reward_item_id`        | string | ID of the reward item associated with the badge. |
| `reward_item_name`      | string | Name of the reward item.                         |
| `reward_item_threshold` | number | Threshold value for the reward item.             |
| `image_url`             | string | URL of the badge image.                          |
| `client_id`             | string | ID of the client associated with the badge.      |
| `profile_id`            | string | ID of the profile receiving the badge.           |
| `profile_custom_id`     | string | Custom identifier for the profile.               |
| `created_at`            | string | Timestamp when the event was created.            |

<br />

## `user-quest-task-progressed`

**Payload Structure:**

```json
{
    "id": "f5967a2f-6fae-4801-9708-189ec59200c9",
    "event": "user-quest-task-progressed",
    "data": {
        "user_quest_task_id": "38a70a0a-c578-4a86-a178-410d8ba58415",
        "user_quest_id": "5998109b-403a-4e88-b38b-1cc98bce9b9e",
        "quest_task_id": "e60c13a4-fe32-4798-b803-4db143355d00",
        "quest_id": "82c81919-c413-41c7-94a8-927040197e27",
        "custom_increment": null,
        "custom_progress": null,
        "client_id": "client-id",
        "profile_id": "profile-id",
        "nickname": "Composed Keeper"
    },
    "created_at": "2024-12-18T12:40:32.993163+00:00"
}
```

**Field Descriptions:**

| Field                | Type   | Description                                |
| -------------------- | ------ | ------------------------------------------ |
| `id`                 | string | Unique identifier for the webhook event.   |
| `event`              | string | The event type.                            |
| `user_quest_task_id` | string | ID of the user quest task.                 |
| `user_quest_id`      | string | ID of the user quest.                      |
| `quest_task_id`      | string | ID of the quest task.                      |
| `quest_id`           | string | ID of the quest.                           |
| `custom_increment`   | number | Custom increment applied to task progress. |
| `custom_progress`    | number | Custom progress value set for the task.    |
| `client_id`          | string | ID of the client.                          |
| `profile_id`         | string | ID of the profile.                         |
| `nickname`           | string | Nickname of the profile.                   |
| `created_at`         | string | Timestamp when the event was created.      |

<br />

### `user-quest-task-completed`

**Payload Structure:**

```json
{
    "id": "e92490c7-934a-477e-9423-62832263bb83",
    "event": "user-quest-task-completed",
    "data": {
        "user_quest_task_id": "65427b29-5b53-4452-9f79-dda23b4051fa",
        "user_quest_id": "e7ca598c-0feb-4385-9a83-525b5bff01b5",
        "quest_task_id": "74006b3b-5b86-4798-9a57-7b0a654b7515",
        "quest_id": "48402f0c-ea5f-4d3f-bedc-e754ec21f1d8",
        "created_at": "2024-12-18T12:28:24Z",
        "completed_at": "2024-12-18T12:40:04Z",
        "status": "completed",
        "progress": 3,
        "client_id": "client-id",
        "profile_id": "profile-id",
        "nickname": "Composed Keeper"
    },
    "created_at": "2024-12-18T12:41:24.826896+00:00"
}
```

<br />

**Field Descriptions:**

| Field                | Type   | Description                              |
| -------------------- | ------ | ---------------------------------------- |
| `id`                 | string | Unique identifier for the webhook event. |
| `event`              | string | The event type.                          |
| `user_quest_task_id` | string | ID of the user quest task.               |
| `user_quest_id`      | string | ID of the user quest.                    |
| `quest_task_id`      | string | ID of the quest task.                    |
| `quest_id`           | string | ID of the quest.                         |
| `created_at`         | string | Timestamp when the event was created.    |
| `completed_at`       | string | Timestamp when the task was completed.   |
| `status`             | string | Status of the task.                      |
| `progress`           | number | Progress made on the task.               |
| `client_id`          | string | ID of the client.                        |
| `profile_id`         | string | ID of the profile.                       |
| `nickname`           | string | Nickname of the profile.                 |

<br />

## `user-quest-completed`

### Payload Example:

```json
{
  "id": "0abc42d4-6520-47f4-9896-5a485642d4a7",
  "event": "user-quest-completed",
  "data": {
    "user_quest_id": "e7ca598c-0feb-4385-9a83-525b5bff01b5",
    "profile_id": "5f724202-246d-439b-8250-527bed44b6c9",
    "quest_id": "48402f0c-ea5f-4d3f-bedc-e754ec21f1d8",
    "quest_task_ids": ["74006b3b-5b86-4798-9a57-7b0a654b7515"],
    "created_at": "2024-12-18T12:28:24Z",
    "completed_at": "2024-12-18T12:40:04Z",
    "active_until": null,
    "timer_expired": false,
    "user_quest_task_ids": ["65427b29-5b53-4452-9f79-dda23b4051fa"],
    "status": "completed",
    "rewards_status": "unclaimed",
    "rewards_claimed_at": null,
    "client_id": "8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS",
    "nickname": "Composed Keeper"
  },
  "created_at": "2024-12-18T12:41:24.825620+00:00"
}
```

### Field Descriptions:

| Field Name                 | Type       | Description                                                          |
| -------------------------- | ---------- | -------------------------------------------------------------------- |
| `id`                       | `string`   | Unique identifier for the event.                                     |
| `event`                    | `string`   | Event type (`user-quest-completed`).                                 |
| `data.user_quest_id`       | `string`   | Unique identifier for the user quest.                                |
| `data.profile_id`          | `string`   | Unique identifier for the user profile.                              |
| `data.quest_id`            | `string`   | Unique identifier for the quest.                                     |
| `data.quest_task_ids`      | `array`    | List of unique quest task identifiers associated with this quest.    |
| `data.created_at`          | `datetime` | Timestamp indicating when the user quest was created.                |
| `data.completed_at`        | `datetime` | Timestamp indicating when the user quest was completed.              |
| `data.active_until`        | `datetime` | Indicates until when the quest was active (if applicable).           |
| `data.timer_expired`       | `boolean`  | Indicates if the quest timer expired.                                |
| `data.user_quest_task_ids` | `array`    | List of unique user quest task identifiers completed for this quest. |
| `data.status`              | `string`   | Status of the quest completion (e.g., `completed`).                  |
| `data.rewards_status`      | `string`   | Status of rewards (e.g., `unclaimed`).                               |
| `data.rewards_claimed_at`  | `datetime` | Timestamp when rewards were claimed (if applicable).                 |
| `data.client_id`           | `string`   | Client-specific identifier.                                          |
| `data.nickname`            | `string`   | Nickname of the user.                                                |
| `created_at`               | `datetime` | Timestamp when the event was created.                                |

## `user-quest-reward-awarded`

### Payload Example:

```json
{
  "id": "7ff896cd-ac8d-4923-95ae-faf162ad2d1e",
  "event": "user-reward-awarded",
  "data": {
    "reward_transaction_id": "7815655b-03ef-4bb3-8c53-916512bff80c",
    "reward_item_id": "4c7bd24e-e0eb-4e07-8472-72e4f52ec4ae",
    "reward_action_key": "poll-voted",
    "reward_action_id": "3bb7b84a-5bcc-4539-bb52-c36b5d410d03",
    "client_id": "8PqSNDgIVHnXuJuGte1HdvOjOqhCFE1ZCR3qhqaS",
    "reward_item_amount": 100,
    "profile_id": "5f724202-246d-439b-8250-527bed44b6c9",
    "profile_custom_id": "avinash@livelike.com",
    "reward_item_balance": 260,
    "nickname": "Composed Keeper"
  },
  "created_at": "2024-12-18T13:31:03.927324+00:00"
}
```

### Field Descriptions:

| Field Name                   | Type       | Description                                                  |
| ---------------------------- | ---------- | ------------------------------------------------------------ |
| `id`                         | `string`   | Unique identifier for the event.                             |
| `event`                      | `string`   | Event type (`user-reward-awarded`).                          |
| `data.reward_transaction_id` | `string`   | Unique identifier for the reward transaction.                |
| `data.reward_item_id`        | `string`   | Unique identifier for the reward item.                       |
| `data.reward_action_key`     | `string`   | Key representing the action associated with the reward.      |
| `data.reward_action_id`      | `string`   | Unique identifier for the action associated with the reward. |
| `data.client_id`             | `string`   | Client-specific identifier.                                  |
| `data.reward_item_amount`    | `integer`  | Amount of reward items awarded.                              |
| `data.profile_id`            | `string`   | Unique identifier for the user profile.                      |
| `data.profile_custom_id`     | `string`   | Custom identifier for the user profile.                      |
| `data.reward_item_balance`   | `integer`  | Current balance of the reward item.                          |
| `data.nickname`              | `string`   | Nickname of the user.                                        |
| `created_at`                 | `datetime` | Timestamp when the event was created.                        |

## `comment-reply-created`

### Payload Example:

```json json
{
  "id": "d611c646-eda9-44ff-84c1-38521775e43c",
  "event": "comment-reply-created",
  "data": {
    "reply_comment_id": "9fc9e53d-0325-467a-9b83-83a8c62e572b",
    "reply_author_id": "1da10aea-96b9-4842-83b7-257ed3953804",
    "reply_author_nickname": "Humble Hamster",
    "reply_author_image_url": null,
    "reply_text": "Test Comment Reply 2",
    "comment_id": "51cc5522-6967-46ff-8edb-afbe90e5e3d5",
    "profile_id": "947d3a03-f87f-4146-8e32-043db3fdd25f",
    "author_nickname": "Swift Zebra",
    "author_image_url": null,
    "comment_text": "Test Comment",
    "client_id": "FVQI5U57tfCyDV99YjhF3ExdlpiObg5JASvy81Mu",
    "created_at": "2025-06-03T08:00:20.567272Z"
  },
  "created_at": "2025-06-03T08:00:20.766704+00:00"
}
```

### Field Descriptions

| Field Name                   | Type       | Description                                                             |
| :--------------------------- | :--------- | :---------------------------------------------------------------------- |
| `id`                         | `string`   | Unique identifier for the event                                         |
| `event`                      | `string`   | Event type {`comment-reply-created`}                                    |
| `data.reply_comment_id`      | `string`   | Unique identifier for the comment reply                                 |
| `data.reply_author_id`       | `string`   | Unique identifier for the author of the new comment reply               |
| `data.reply_author_nickname` | `string`   | Nickname for the author of the new comment reply                        |
| `data.reply_text`            | `string`   | The actual text content of the new comment reply                        |
| `data.profile_id`            | `string`   | Unique identifier for the author of the original comment                |
| `data.comment_id`            | `string`   | Unique identifier for the original comment to which the reply was given |
| `data.author_nickname`       | `string`   | Nickname for the author of the original comment                         |
| `data.author_image_url`      | `string`   | The url for the profile image for the author of the original comment    |
| `data.comment_text`          | `string`   | The actual text content of the original comment                         |
| `data.client_id`             | `string`   | Client-specific identifier                                              |
| `data.created_at`            | `string`   | Timestamp when the comment reply was created                            |
| `created_at`                 | `datetime` | Timestamp when the event was created                                    |

## `comment-mention-created`

### Payload Example:

```json
{
  "id": "26059f13-9864-4507-a19c-5891bbac5beb",
  "event": "comment-mention-created",
  "data": {
    "profile_id": "947d3a03-f87f-4146-8e32-043db3fdd25f",
    "mentioned_by_id": "ce74ad6c-496d-48da-85a6-9b6d83367598",
    "comment_id": "ce1b34f3-2cdf-4145-87ee-e9c2279f838f",
    "comment_text": "Hey @Swift and @Witty, how are you?",
    "start_index": 4,
    "end_index": 9,
    "client_id": "FVQI5U57tfCyDV99YjhF3ExdlpiObg5JASvy81Mu",
    "created_at": "2025-09-10T06:27:03.349873Z"
  },
  "created_at": "2025-09-10T06:27:03.629615+00:00"
}
```

### Field Descriptions

| Field Name             | Type       | Description                                                   |
| :--------------------- | :--------- | :------------------------------------------------------------ |
| `id`                   | `string`   | Unique identifier for the event                               |
| `event`                | `string`   | Event type {`comment-mention-created`}                        |
| `data.profile_id`      | `string`   | Unique identifier for the mentioned profile                   |
| `data.mentioned_by_id` | `string`   | Unique identifier for the mentioned_by profile                |
| `data.comment_id`      | `string`   | Unique identifier for the comment                             |
| `data.comment_text`    | `string`   | Text content of the comment in which mentionws were created   |
| `data.start_index`     | `string`   | Starting index of the mention placeholder in the comment text |
| `data.end_index`       | `string`   | Ending index of the mention placeholder in the comment text   |
| `data.client_id`       | `string`   | Client-specific identifier                                    |
| `data.created_at`      | `datetime` | Timestamp when the comment mention was created                |
| `created_at`           | `datetime` | Timestamp when the event was created                          |

## `profile-relationship-created`

### Payload Example:

```json
{
  "id": "81b4d144-2936-44b7-867b-8c8740dc6159",
  "event": "profile-relationship-created",
  "data": {
    "relationship_type": "follow",
    "to_profile_id": "31d9b4b0-7ef6-44f8-911c-96035700c7d8",
    "is_active": true,
    "profile_id": "ce74ad6c-496d-48da-85a6-9b6d83367598",
    "client_id": "FVQI5U57tfCyDV99YjhF3ExdlpiObg5JASvy81Mu",
    "created_at": "2025-09-10T07:01:46Z"
  },
  "created_at": "2025-09-10T07:02:16.062427+00:00"
}
```

### Field Descriptions

| Field Name               | Type       | Description                                                |
| :----------------------- | :--------- | :--------------------------------------------------------- |
| `id`                     | `string`   | Unique identifier for the event                            |
| `event`                  | `string`   | Event type {`profile-relationship-created`}                |
| `data.relationship_type` | `string`   | Unique key for profile relationship type                   |
| `data.to_profile_id`     | `string`   | Unique identifier for the from profile in the relationship |
| `data.is_active`         | `boolean`  | Active status for the profile relationship                 |
| `data.profile_id`        | `string`   | Unique identifier for the to profile in the relationship   |
| `data.client_id`         | `string`   | Client-specific identifier                                 |
| `data.created_at`        | `datetime` | Timestamp when the profile relationship was created        |
| `created_at`             | `datetime` | Timestamp when the event was created                       |

***

## Notes

1. All id fields are UUIDs (Universally Unique Identifiers).
2. Timestamps follow the ISO 8601 format (YYYY-MM-DDTHH:MM:SSZ).
3. Additional events will follow a similar structure and will be documented as they are added.
