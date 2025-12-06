---
title: Trending Comments
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: list-comments
      title: List comments
      type: endpoint
---
Each comment is assigned a trending score that summarizes the replies and reactions it has received recently. Lists of comments can be ordered by their `trending_score` to show comments sorted by their trending score, see the [ordering comments by trending](https://docs.livelike.com/reference/list-comments#trending-comments)  docs for details.

## Scoring calculation

The default trending score is calculate as `(WR * R + WRe * Re)  * e^(-λt)` where the terms are:

* `R` = Number of direct replies
* `WR` = Weight of replies. Default = 2
* `Re` = Number of reactions
* `WRe` = Weight of reactions. Default = 1
* `t` = Time elapsed since the comment was posted, in minutes
* `λ` = Decay constant, controls how quickly older comments lose relevance. Default = 0.1
  * Higher `λ`, faster Decay (e.g. λ = 0.1)
  * Lower `λ`, slower Decay (e.g. λ = 0.01)

## Customizing the scoring calculation

The weights (WR, WRe) and the decay constant (λ) can be customized for each client application, allowing flexibility to fine-tune how comment popularity and recency influence the trending score.

```curl
curl -X PATCH https://cf-blast.livelikecdn.com/api/v1/applications/<client_id>/ \
  -H "Authorization: Token <Bearer_Token>" \
  -H "Content-Type: application/json" \
  -d '{
  "comment_trending_score_factors": {
  "reply_weight": 1,
  "reaction_weight": 3,
  "decay_constant": 0.05,
 }
  }'
```

If any comment's **Number of direct replies** and **Number of reactions** are zero, the trending score isn’t calculated because the formula will always produce zero hence **trending_score** ends up as the default value, which is null.

<br />
