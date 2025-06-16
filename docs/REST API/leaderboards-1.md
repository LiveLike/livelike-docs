---
title: Leaderboards
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Leaderboards allow users to compete and see how they stack up against each other. Once a leaderboard has been associated with a Program, users who earn rewards in that program will have them counted toward their ranks on that leaderboard.

A program can have many leaderboards associated, and a leaderboard can be linked with many programs. This allows you to better capture your own experience's structure better, such as allowing all-time, seasonal, or single event leaderboards, and even mixing and matching them.

 [To learn more about how Leaderboards work as a product, click here](https://docs.livelike.com/docs/leaderboards)
[block:api-header]
{
  "title": "Getting leaderboards associated with a program"
}
[/block]
Leaderboards associated with a program can be retrieved by getting the program's details. In the response you will find an array of leaderboard objects under the `leaderboards` property.
[block:code]
{
  "codes": [
    {
      "code": "GET /programs/{\"program id\"}/program.json",
      "language": "python",
      "name": "Request"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "title": "",
  "body": "[See how we use this call in our own SDKs here](https://docs.livelike.com/docs/leaderboards#getting-leaderboards-associated-with-a-program)"
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboard details"
}
[/block]
Getting leaderboard details can be achieved by using the request below. Leaderboard details can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.
[block:code]
{
  "codes": [
    {
      "code": "GET /api/v1/leaderboards/{\"leaderboard id\"}",
      "language": "python",
      "name": "Request"
    }
  ]
}
[/block]

[block:callout]
{
  "type": "warning",
  "body": "[See how we use this call in our own SDKs here](https://docs.livelike.com/docs/leaderboards#getting-leaderboard-details)"
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboard entries"
}
[/block]
A user that competes is considered a leaderboard entry. Retrieving leaderboard entries returns a paginated list of twenty leaderboard entry objects at maximum. 

**Getting leaderboard entry url**
In order to make a leaderboard entries request you will need to acquire a leaderboard entries url and an access token. A leaderboard entries url can be retrieved using two of the following ways.
1. From the response of the leaderboard detail request mentioned above, under the property `entries_url`.  This url, when used in a `GET` request will always return the first page of leaderboard entries. 
2. Every leaderboard entries result will contain properties `next` and `previous`. These are optional urls that can be used in conjunction with your access token to retrieve more leaderboard entries.
[block:code]
{
  "codes": [
    {
      "code": "GET /services/leaderboards/{\"leaderboard id\"}/entries",
      "language": "python",
      "name": "Request"
    }
  ]
}
[/block]
**Working with leaderboard entry url**
Once a leaderboard entries url is acquired, you can use it to retrieve sequential pages using the `start` parameter. The `start` parameter signifies an index from which you would like to receive results. 
[block:code]
{
  "codes": [
    {
      "code": "GET /services/leaderboards/{\"leaderboard id\"}/entries?start={\"start index\"}",
      "language": "python"
    }
  ]
}
[/block]
For example, if there are 50 leaderboard entries and you would like to receive entries 10 - 30, skipping the top 10, you would do the following `GET` request shown below. 
[block:code]
{
  "codes": [
    {
      "code": "GET /services/leaderboards/{\"leaderboard id\"}/entries?start=10",
      "language": "python"
    }
  ]
}
[/block]