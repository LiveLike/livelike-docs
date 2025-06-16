---
title: List Leaderboard Entries
excerpt: >-
  A user that competes is considered a leaderboard entry. Retrieving leaderboard
  entries returns a paginated list of twenty leaderboard entry objects at
  maximum.
api:
  file: leaderboards.json
  operationId: getting-leaderboard-entries
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
**Getting leaderboard entry url**\
In order to make a leaderboard entries request you will need to acquire a leaderboard entries url and an access token. A leaderboard entries url can be retrieved using two of the following ways.

1. From the response of the leaderboard detail request mentioned above, under the property `entries_url`.  This url, when used in a `GET` request will always return the first page of leaderboard entries. 
2. Every leaderboard entries result will contain properties `next` and `previous`. These are optional urls that can be used in conjunction with your access token to retrieve more leaderboard entries.

**Working with leaderboard entry url**\
Once a leaderboard entries url is acquired, you can use it to retrieve sequential pages using the `offset` parameter. The `offset` parameter signifies an index from which you would like to receive results. 

```python
GET https://cf-blast.livelikecdn.com/api/v1/leaderboards/{"leaderboard id"}/entries?offset={"start index"}
```
