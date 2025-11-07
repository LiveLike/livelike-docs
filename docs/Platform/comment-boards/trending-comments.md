---
title: Trending Comments
deprecated: false
hidden: true
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

```curl
curl -X PATCH https://cf-blast.dig.livelikecdn.com/api/v1/applications/GH4E2uZ8ED0rJUS1k3vQFJbiBjR7iRsrFrd5wI9F/ \
  -H "Authorization: Token <Bearer_Token>" \
  -H "Content-Type: application/json" \
  -d '{
    "comment_trending_score_factors": {
      "reply_weight": 1,
  		"reaction_weight": 3,
      "decay_constant": 0.5,
    }
  }'
```

<br />
