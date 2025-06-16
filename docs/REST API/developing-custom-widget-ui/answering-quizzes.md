---
title: Answering Quizzes
excerpt: How to answer text quizzes and image quizzes with the REST API
deprecated: false
hidden: false
metadata:
  title: Answering Quizzes | REST API | LiveLike Developer Hub
  description: >-
    Answers can be added to Text Quiz and Image Quiz widgets directly through
    the REST API. Learn how to answer quizzes.
  robots: index
next:
  description: ''
---
Answers can be added to Text Quiz and Image Quiz widgets directly through the REST API. Usually the SDK calls the quiz answering API's for users interacting with the built-in widgets, but if you are building your own widgets, then your integration code will have to call these API's on the behalf of users.

## Create a Quiz Answer

Each quiz has a list of choices that can be voted for in its `choices` field. A new answer is created by making a POST request to the URL in the `answer_url` field on the desired choice. Each choice has its own unique answer URL, the request body may be empty, and a profile access token is required. Here is an example text quiz widget, with unrelated fields omitted:

```json text-quiz-example.json
{
  "id": "example-text-quiz",
  "question": "Who holds the record for most touchdowns in NFL history?",
  "choices": [
    {
      "id": "example-choice-1",
      "description": "Fran Tarkenton",
      "is_correct": false,
      "answer_count": 0,
      "answer_url": "https://livelike.example.com/answer-service/example-choice-1/"
    },
    {
      "id": "example-choice-2",
      "description": "Peyton Manning",
      "is_correct": true,
      "answer_count": 0,
      "answer_url": "https://livelike.example.com/answer-service/example-choice-2/"
    },
    {
      "id": "example-choice-3",
      "description": "Tom Brady",
      "is_correct": false,
      "answer_count": 0,
      "answer_url": "https://livelike.example.com/answer-service/example-choice-3/"
    },
    {
      "id": "example-choice-4",
      "description": "Matt Ryan",
      "is_correct": false,
      "answer_count": 0,
      "answer_url": "https://livelike.example.com/answer-service/example-choice-4/"
    }
  ],
  "subscribe_channel": "text-quizzes:example-text-quiz",
  "program_id": "example-program"
}
```

The above widget has four choices to choose from. Since each choice has its own answer URL, creating a new answer doesn't need a request body. Just make a POST request to the choice's answer URL. So if you wanted the first choice to be your answer, you would make this request:

> ❗️ Avoid building or predicting answer URLs
>
> Each `answer_url` is unique to its choice, and might vary over time. Instead of constructing URLs client-side, please send requests to the URLs in the response verbatim.

```python addvote.py
# Set up auth headers, profile contains current user's LiveLike profile
headers = {'Authorization': f"Bearer {profile['access_token']}"}

# Assume example_quiz contains the example widget from earlier
requests.post(example_quiz['choices'][0]['answer_url'], headers=headers)
```

> 🚧 Authorization is required!
>
> Quizzes cannot be answered anonymously. Make sure to include the user's Profile Access Token in the Authorization header in requests working with quiz answers.
