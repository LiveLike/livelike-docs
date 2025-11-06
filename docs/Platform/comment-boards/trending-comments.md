---
title: Trending Comments
deprecated: false
hidden: true
metadata:
  robots: index
---
Each comment is assigned a trending score that summarizes the replies and reactions it has received recently. That score is continuously updated. Lists of comments can be ordered by their `trending_score` to show comments sorted by their trending score.

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

TODO
