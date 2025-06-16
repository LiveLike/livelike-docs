---
title: Voting on Polls
excerpt: How to vote on text polls and image polls with the REST API
deprecated: false
hidden: false
metadata:
  title: Voting on Polls | REST API | LiveLike Developer Hub
  description: >-
    Votes can be added to Text Polls and Image Polls directly through the REST
    API. Learn how to vote on polls with the REST API.
  robots: index
next:
  description: ''
---
Votes can be added to Text Polls and Image Polls directly through the REST API. Usually the SDK calls the poll voting API's for users interacting with the built-in widgets, but if you are building your own widgets, then your integration code will have to call the poll voting API's on the behalf of users.

## Create a Poll Vote

Each poll has a list of options that can be voted for in its `options` field. A new vote is created by making a POST request to the URL in the `vote_url` field on the desired option. Each poll option has its own unique Vote URL, the request body may be empty, and a profile access token is required. Here is an example text poll widget, with unrelated fields omitted:

```json text-poll-example.json
{
  "id": "example-text-poll",
  "question": "Is this Eli Manning's last game with the giants?",
  "options": [
    {
      "id": "example-option-1",
      "description": "For sure! He's done.",
      "vote_count": 0,
      "vote_url": "https://livelike.example.com/vote-for-option/example-option-1/"
    },
    {
      "id": "example-option-2",
      "description": "No. He still has a lot left in the tank!",
      "vote_count": 0,
      "vote_url": "https://livelike.example.com/vote-for-option/example-option-2/"
    }
  ],
  "url": "https://livelike.example.com/api/v0/text-polls/example-text-poll/",
  "program_id": "example-program"
}
```

The above widget has two options to vote for. Since each option has its own Vote URL, creating a new vote doesn't need a request body. Just make a POST request to the option's vote URL. So if you wanted to vote for the first option, you would make this request:

> ❗️ Avoid building or predicting vote URLs
>
> Each `vote_url` is unique to its option, and might vary over time. Instead of constructing URLs client-side, please send requests to the URLs in the response verbatim.

```python addvote.py
# Set up auth headers, profile contains current user's LiveLike profile
vote_headers = {'Authorization': f"Bearer {profile['access_token']}"}

# Assume example_poll contains the example poll from earlier
requests.post(example_poll['options'][0]['vote_url'], headers=vote_headers)
```

> 🚧 Authorization is required!
>
> Poll Votes cannot be created or updated anonymously. Make sure to include the user's Profile Access Token in the Authorization header in requests working with poll votes.

## Update a Poll Vote

If you have already voted on a poll, you can change the option you voted for. Each poll vote has a `url` property. A PUT request can be made to vote's `url` field with a body parameter named `option_id` containing the ID of the option you would like to change your vote to. Here is an example text poll vote for someone who voted on the first option in the example poll:

```json example-text-poll-vote.json
{
  "id": "example-text-poll-vote",
  "url": "https://livelike.example.com/api/v1/text-poll-votes/example-text-poll-vote/",
  "option_id": "example-option-1"
}
```

If the person who created that vote wanted to change their vote to the second option, they would make this request:

```shell change-vote.sh
curl -XPUT "$VOTE_URL" \
  -H "Authorization: Bearer $PROFILE_ACCESS_TOKEN" \
  -d "option_id=example-option-2"
```
