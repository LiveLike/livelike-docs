---
title: Comment Mentions
excerpt: The Mentions feature lets users tag specific profiles in a comment.
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - title: Send Comments with Mentions
      type: link
      url: https://docs.livelike.com/update/reference/create-a-comment#/
    - title: Fetch Comments with MentionsFetch Chat messages with Mentions
      type: link
      url: https://docs.livelike.com/update/reference/create-a-comment#/
---
## Overview

The Comment Mentions feature allows your users to tag specific profiles inside their comments, creating more interactive and engaging conversations. Mentions make it easy to bring people into discussions, just like the familiar “@mention” experience on popular social platforms. Mentions are included when a comment is created and are also returned in the GET API responses.

## How "Mention" works

Client send structured mention data in the POST request when creating a chat message.
This includes:

* The profile being mentioned (`mentioned_profile_id` or `mentioned_profile_custom_id`)
* The `start_index` and `end_index` : refer to the character positions of the mention placeholder in the message text.

```curl
POST /api/v1/comments/
{
  "comment_board_id": "4ec4cdc9-8b80-4ef1-aff2-610125141035",
  "text": "hello @mention1_placeholder, How are you?",
  "mentions": [
    {
      "mentioned_profile_id": "6f273566-8683-4764-b365-3f9b559d70a6",
      // or mentioned_profile_custom_id
      "start_index": 6,
      "end_index": 27
    }
  ]
}
```

At render time, placeholder text in the comment can be replaced with the nickname of the mentioned profile.

#### Validation Rules:

1. Max 10 mentions per comment
2. Indices must be within text bounds and non-overlapping
3. Provide either `mentioned_profile_id` or `mentioned_profile_custom_id` (not both)
4. `mentioned_profile_custom_id` must resolve to a valid profile
5. Mention is not allowed if:

   * The mentioner has blocked the mentioned profile
   * The mentioned profile has blocked the mentioner