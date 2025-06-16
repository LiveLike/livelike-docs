---
title: Leaderboards
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: JavaScript Leaderboards | LiveLike Developer Hub | JavaScript SDK
  description: >-
    JavaScript leaderboards allow users to compete and see how they stack up
    against each other. Learn more about configuring JavaScript leaderboards.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "What are Leaderboards? How to setup a leaderboard?",
  "body": "Refer our core [leaderboards](leaderboards) documentation."
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboards associated with a program"
}
[/block]
You have the option to retrieve all leaderboards associated to a program by using the code samples below. This function will return an array of leaderboards.

**API Definition:** [getLeaderboards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboards)
[block:code]
{
  "codes": [
    {
      "code": "import { getLeaderboards } from \"@livelike/javascript\"\n\ngetLeaderboards({\n  programId: \"<program id>\"\n}).then(leaderboards => console.log(leaderboards));",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboard details"
}
[/block]
If you know a leaderboard id, you are able to get its details by using the code samples below. This can be useful if you would like to know the name of the leaderboard or the type of reward a user can earn.

**API Definition:** [getLeaderboard](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboard)
[block:code]
{
  "codes": [
    {
      "code": "import { getLeaderboard } from \"@livelike/javascript\"\n\ngetLeaderboard({leaderboardId: \"<leaderboard id>\"})\n\t.then(leaderboard => console.log(leaderboard));",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboard entries"
}
[/block]
A user that competes is considered a leaderboard entry. Use the code samples below to retrieve leaderboard entries for a specific leaderboard. Due to the nature of leaderboard entries growing to a very high number, this call is paginated with each page returning 20 leaderboard entries.

**API Definition:** [getLeaderboardEntries](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardEntries) 
[block:code]
{
  "codes": [
    {
      "code": "import { getLeaderboardEntries } from \"@livelike/javascript\"\n\ngetLeaderboardEntries({\n  leaderboardId: \"<leaderboard id>\",\n  profileIds: [\"<profileId1>\",\"<profileId2>\"]\n}).then(leaderboardEntries => console.log(leaderboardEntries));",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting leaderboard entry for a given profile"
}
[/block]
Details about a leaderboard entry can be retrieved by providing a profile id and a leaderboard id. This can be useful if there is a leaderboard entry you are interested in keeping track of.

 **API Definition:** [getLeaderboardProfileRank](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardProfileRank)
[block:code]
{
  "codes": [
    {
      "code": "import { getLeaderboardProfileRank } from \"@livelike/javascript\"\n\ngetLeaderboardProfileRank({\n  leaderboardId: \"<leaderboard id>\",\n  profileId: \"<profile id>\"\n}).then(profileRank => console.log(profileRank));",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Getting a leaderboard entry for the current user profile"
}
[/block]
Retrieving details about the current user's profile can be done using the code samples below. This can be used to look up the current user's ranking in a specific leaderboard.

 **API Definition:** [getLeaderboardProfileRank](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getLeaderboardProfileRank)
[block:code]
{
  "codes": [
    {
      "code": "import { getLeaderboardProfileRank, userProfile } from \"@livelike/javascript\"\n\ngetLeaderboardProfileRank({\n  leaderboardId: \"<leaderboard id>\",\n  profileId: userProfile.id\n}).then(profileRank => console.log(profileRank));\n",
      "language": "javascript",
      "name": "JavaScript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Leaderboards a given profile is ranked on"
}
[/block]
Integrators can fetch the leaderboards a given profile is ranked on.

 **API Definition:** [getProfileLeaderboards](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileLeaderboards)
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileLeaderboards } from \"@livelike/javascript\"\n\n// leaderboard list for current profile\ngetProfileLeaderboards()\n.then(leaderboards => console.log(leaderboards))\n \n// leaderboard list for a given profileId\ngetProfileLeaderboards({\n  profileId: \"<profile-id>\"\n}).then(leaderboards => console.log(leaderboards))",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Get Leaderboard views for a given profile"
}
[/block]
Integrators can fetch the leaderboard views for a given profile.

 **API Definition:** [getProfileLeaderboardViews](https://livelike-doc-redirect-url.herokuapp.com/javascript?keyword=getProfileLeaderboardViews)
[block:code]
{
  "codes": [
    {
      "code": "import { getProfileLeaderboardViews } from \"@livelike/javascript\"\n\n// leaderboard views for current profile\ngetProfileLeaderboardViews()\n.then(leaderboardviews => console.log(leaderboardviews))\n \n// leaderboard views for a given profileId\ngetProfileLeaderboardViews({\n  profileId: \"<profile-id>\"\n}).then(leaderboardviews => console.log(leaderboardviews))",
      "language": "javascript"
    }
  ]
}
[/block]