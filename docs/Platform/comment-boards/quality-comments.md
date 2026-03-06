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

1. Each application can define its own criteria for quality comments using the **CommentQualityRules** configuration model.
2. These rules determine how the system identifies **high quality comments**.
3. Common signals used in the rules include:
   1. AI moderation signals
      1. Sentiment analysis (positive, neutral, negative) - Calculated as a score ranging from -1 to 1, -1 being the most negative and 1 being the most positive.
      2. Toxicity analysis (high, medium, low) - Calculated as a score ranging from 0 to 1, 0 being the least toxic and 1 being the most toxic.
   2. **Content Signals**
      1. Minimum character count - Whitespaces excluded from this count
      2. Allowed or disallowed characters
      3. Emoji to text ratio
4. These signals help distinguish meaningful fan participation from spam, noise or low-effort messages.

<br />

## System Tags Comments as High Quality

1. Based on the configured rules, the system assigns a quality flag to each comment. **(is_high_quality = true | false)**
2. This flag is returned in the Comment List API allowing clients to filter comments that meet the quality criteria.

<br />

## Filter Comments by Engagement Using Trending Score

1. Clients can further refine results using trending score filters.
2. Trending score reflects how much engagement a comment is receiving.
3. Available filters:
   1. **trending_score_gte** - return comments with scores greater than or equal to a value
   2. **trending_score_lte** - return comments with scores less than or equal to a value
   3. Example: trending_score_gte=3; This helps surface comments that are gaining attention or engagement.

<br />

## Retrieve comments from multiple comment boards

1. Clients can request comments from multiple comment boards in a single API call. `comment_board_id={'<id_1>'}`; `comment_board_id={'<id_2>'}`.
2. This is useful for Events with multiple chat rooms or Aggregating conversations across different topics or moments.

<br />

## Limit Comments per board

1. To ensure balanced results, clients can limit the number of comments returned per board.
2. For example: per_board_limit=5; This returns up to 5 comments from each comment board, preventing one board from dominating the results.

<br />

## Order the results

1. Clients can apply a sorting parameter to control the order in which comments are returned.
2. Example use cases:
   1. Sort by trending score to highlight popular comments
   2. Sort by recency to show the latest quality comments

<br />

For more details on the List Comments API,  please check this out: <Anchor label="List Comments API" target="_blank" href="https://docs.livelike.com/update/reference/list-comments">List Comments API</Anchor>

<br />

## Implementation Example

<br />

### Top Fan Comments

1. Top Fan Comments: Highlight the most meaningful comments from fans during an event.
2. How it works: The client fetches comments that are marked high quality & have a valid trending score.
3. UI Displayed as:
   1. Top Comments section
   2. Pinned reactions panel
   3. Featured fan voices
   4. Fan reaction rail
4. Example Experience: During a live sports match, the platform shows Top 5 fan reactions that add meaningful discussion instead of short or spam-like messages.

<br />

### Noise Reduction

1. Only comments marked as high quality are displayed.
2. UI Displayed as:
   1. Curated comment feed
   2.  Premium discussion mode
3. Example Experience: Instead of showing every message, the platform surfaces comments that add value to the conversation.

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
