---
title: Quality Comments
deprecated: false
hidden: false
metadata:
  robots: index
---
The Quality Comments feature allows clients to programmatically retrieve the most meaningful, engaging, and high-signal comments from one or multiple comment boards. This helps highlight the best fan comments, reduce noise, and power experiences such as Top Comments or Highlights. This capability is powered by comment quality signals.

<br />

# Key Capabilities

<br />

## Comment Quality Rules

* Each application can define its own criteria for quality comments using the **CommentQualityRules** configuration model.
* These rules determine how the system identifies **high quality comments**.
* Common signals used in the rules include:

  **AI moderation signals**
  * Sentiment analysis (positive, neutral, negative) - Calculated as a score ranging from -1 to 1, -1 being the most negative and 1 being the most positive.
  * Toxicity analysis (high, medium, low) - Calculated as a score ranging from 0 to 1, 0 being the least toxic and 1 being the most toxic.
  **Content Signals**
  * Minimum character count - Whitespaces excluded from this count
  * Allowed or disallowed characters
  * Emoji to text ratio
* These signals help distinguish **meaningful fan participation** from spam, noise or low-effort messages.

<br />

## System Tags Comments as High Quality

* Based on the configured rules, the system assigns a quality flag to each comment. **(is_high_quality = true | false)**
* This flag is returned in the Comment List API allowing clients to filter comments that meet the quality criteria.

<br />

## Filter Comments by Engagement Using Trending Score

* Clients can further refine results using trending score filters.
* Trending score reflects how much engagement a comment is receiving.
* Available filters:
  * **trending_score_gte** - return comments with scores greater than or equal to a value
  * **trending_score_lte** - return comments with scores less than or equal to a value
  * Example: trending_score_gte=3; This helps surface comments that are gaining attention or engagement.

<br />

## Retrieve comments from multiple comment boards

* Clients can request comments from multiple comment boards in a single API call. comment_board_id={'<id_1>'}; comment_board_id={'<id_2>'}.
* This is useful for Events with multiple chat rooms or Aggregating conversations across different topics or moments.

<br />

## Limit Comments per board

* To ensure balanced results, clients can limit the number of comments returned per board.
* For example: per_board_limit=5; This returns up to 5 comments from each comment board, preventing one board from dominating the results.

<br />

## Order the results

* Clients can apply a sorting parameter to control the order in which comments are returned.
* Example use cases:
  * Sort by trending score to highlight popular comments
  * Sort by recency to show the latest quality comments

<br />

For more details on the List Comments API,  please check this out: <Anchor label="List Comments API" target="_blank" href="https://docs.livelike.com/update/reference/list-comments">List Comments API</Anchor>

<br />

## Implementation Example

<br />

### Top Fan Comments

* **Top Fan Comments:** Highlight the most meaningful comments from fans during an event.
* **How it works:** The client fetches comments that are marked high quality & have a valid trending score.
* **UI Displayed as:**
  * Top Comments section
  * Pinned reactions panel
  * Featured fan voices
  * Fan reaction rail
* **Example Experience:** During a live sports match, the platform shows Top 5 fan reactions that add meaningful discussion instead of short or spam-like messages.

<br />

### Noise Reduction

* Only comments marked as high quality are displayed.
* **UI Displayed as:**
  * Curated comment feed
  * Premium discussion mode
  * **Example Experience:** Instead of showing every message, the platform surfaces comments that add value to the conversation.

<br />

## Best Practices for Clients

* To get the best results from Quality Comments use trending score + quality filter together. This helps surface comments that are both meaningful and engaging.
* Limit comments per board when aggregating feeds. This prevents a single comment board from dominating results.
* Tune quality rules based on your community behavior.  For example: Sports chats may allow more emojis whereas News discussions may require longer messages

<br />

| Feature         | What it Measures                           |
| :-------------- | :----------------------------------------- |
| Quality Comment | Whether a comment is meaningful            |
| Trending Score  | How much engagement a comment is receiving |

While each feature solves a different use case, combing the two can bring out the most effective results.