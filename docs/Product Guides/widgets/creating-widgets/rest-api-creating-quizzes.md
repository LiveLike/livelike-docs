---
title: Creating Quizzes
excerpt: How to create quiz widgets with the REST API
deprecated: false
hidden: false
metadata:
  title: Creating Quizzes | REST API | LiveLike Developer Hub
  description: >-
    Quizzes challenge an audience's knowledge and add game elements your
    experience. Learn how to create quizzes with the REST API.
  robots: index
next:
  description: ''
  pages:
    - type: link
      title: Quiz Widgets Guide
      url: https://docs.livelike.com/docs/widgets#section-trivia-quiz
    - type: basic
      slug: answering-quizzes
      title: Answering Quizzes
---
Quizzes challenge an audience's knowledge and add game elements your experience. The REST API has two types of quizzes: text quizzes and image quizzes. A quiz is made up a question and a list of choices. Quizzes are limited from 2–4 choices, any or all or none of which may be correct. Image quizzes must have an image associated with each choice.

## Create a Quiz

All widgets are created as part of a <Glossary>Program</Glossary> and each program has its own unique ID. To send a quiz widget, a new one must first be created within the program that your audience will be interacting with. When creating a quiz, the `program_id`, `question`, and `choices` body parameters are required.

```python createimagequiz.py
# Configure your Program ID
program_id = "your-program-id"

# Set up authorization headers using your API access token
headers = {'Authorization': f'Bearer {access_token}'} 
           
# Create a new image quiz widget
payload = {
  'program_id': program_id,
  'question': 'Who holds the record for most touchdowns in NFL history?',
  'choices': [
    {
      'image_url': 'https://example.com/image1.png',
      'description': 'Fran Tarkenton',
      'is_correct': false
    },
    {
      'image_url': 'https://example.com/image2.png',
      'description': "Peyton Manning",
      'is_correct': true
    },
    {
      'image_url': 'https://example.com/image3.png',
      'description': 'Tom Brady',
      'is_correct': false
    },
    {
      'image_url': 'https://example.com/image4.png',
      'description': 'Matt Ryan',
      'is_correct': false
    }
  ]
}
r = requests.post('https://cf-blast.livelikecdn.com/api/v1/image-quizzes/', json=payload, headers=headers)
quiz = r.json()
```

Once a widget is created, it will appear in the Pending section of the Producer Studio, but users won't see it yet. A widget has to be published before an audience will see it.

> 📘 More info is in the API reference!
>
> Please see the [Using Widgets](https://docs.livelike.com/v1/reference#widgets-basics) section of the API reference documentation for more details about how widgets are created and published.

## Publish the Quiz

Widgets get published according to the program schedule. Every widget has a `schedule_url` field that can be called to update the schedule. The schedule works by setting a delay on a widget, and once the delay is reached the widget gets published. If you want to publish a widget immediately, use a delay of zero. Here is how you would immediately publish the quiz created earlier:

```python
# Schedule the widget to publish immediately
publish_payload = {'publish_delay': 'P0DT0S'}
requests.put(quiz['schedule_url'], json=publish_payload, headers=headers)
```

> 👍 Specify publish delays in ISO format
>
> The `publish_delay` body parameter is specified in ISO 8601 duration format.

Once the widget is published, it will appear in the History tab in the Producer Studio, and audiences will see it on their devices if they are subscribed to the program.

## Quiz Variations

The REST API supports two quiz variants, text quizzes and image quizzes. They function mostly identically, except for these key differences:

* Image quiz and Text Quiz are two separate API resources
* Image quiz choices require an `image_url` field that text quiz choices do not have

## Answering Quizzes

After a quiz has been created it can be answered by fans. User interactions with quizzes are usually managed by client-side libraries on iOS, Android, or Web, but if you would like to manage that directly then [Answering Quizzes](doc:answering-quizzes) will walk you through how to do so.
