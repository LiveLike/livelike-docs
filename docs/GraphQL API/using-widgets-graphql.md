---
title: Using Widgets (GraphQL)
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: widgets
      title: Widgets
---
Widgets are the set of elements like polls, quizzes, and predictions that can be used to build interactive experiences. Widgets are delivered to audiences in two steps: first they are created, and then they are published. This allows for complex workflows to be managed, so that widgets can be created, scheduled, and edited ahead of time before publishing.

> 📘 Widgets belong to a program
> 
> Before you can create a widget, you must first create a <<glossary:Program>> for it to belong to. You can use the `createProgram` mutation to create a new program now, or learn more about [Programs](doc:programs) in the product docs.

More information about [Widgets](doc:widgets) is available in the product guide.

## Creating Widgets

When a widget is first created, it is considered _pending_. It exists in the system and can be referenced in the API, but has not been published to an audience. Here is some sample mutation for creating a new text poll:

```graphql
mutation NewTextPoll {
  createTextPoll(
    input: {programId: $programId, question: $question, options: $options, timeout: $timeout}
  ) {
    id
    options {
      id
      description
    }
    programId
    status
  }
}
```

Running this mutation will create the poll and it will appear in the Pending tab inside the CMS. After it's created it can be published immediately or scheduled for later. Other mutations for creating widgets include:

- `createImagePoll`
- `createRichPost`

> 📘 Users can create widgets too
> 
> Widgets are often created by server-to-server calls with Producer authorization, but profiles with appropriate permissions can create widgets too. Use the [Roles and Permissions](doc:roles-and-permissions) system with permissions like `create-text-poll` and `publish-text-poll` to enable user-generated widgets in your integration.

## Publishing Widgets

A pending widget has to be _published_ for it to appear in timelines and send pubsub messages. Publishing a widget is done through the `publishWidget` mutation. Here's how a text poll would be published immediately:

```graphql
mutation PublishTextPoll {
  publishWidget(input: {widgetId: $textPollId, kind: TEXT_POLL}) {
    status
    publishedAt
  }
}
```

Publishing a widget can take an optional `publishDelay` input field in ISO duration format which will delay scheduling, so you can schedule a widget to be published sometime in the future. When publishing on a delay, the widget's status will be _scheduled_ until the delay elapses and the widget is published.

## Creating Votes

Votes can be created on Text Polls and Image Polls. Each Poll has a list of options, and a vote can be created for one option. Each option has a unique `optionId`, which is used to create the vote. 

> 🚧 Authorization is required
> 
> Poll Votes cannot be created or updated anonymously. Make sure to include the user's Profile <<glossary:Access Token>> in the Authorization header in requests when working with poll votes.

```graphql
mutation CreatePollVote {
  createPollVote(input: {widgetId: $textPollId, kind: TEXT_POLL, optionId: $optionId}) {
    createdAt
    id
    optionId
    profileId
    widgetId
    widgetKind
  }
}
```

## Updating Votes

Once a poll vote has been created, another vote on the same poll from the same user cannot be created. To change the vote, the vote must be updated. To do so, the `id` of the original vote creation response is used, as well as an `optionId` other than the `optionId` of the originally created vote.

```graphql
mutation UpdatePollVote {
  updatePollVote(input: {id: $voteId, widgetId: $textPollId, kind: TEXT_POLL, optionId: $optionId}) {
    createdAt
    id
    optionId
    profileId
    widgetId
    widgetKind
  }
}
```

## Getting Widget Interactions

Once votes have been created, these interactions are recorded and associated with the user profile that made them. Previously vote interactions can then be used to display to the user.

> 📘 Multiple widget interactions can be fetched simultaneously
> 
> The `ids` field in the input is an array of widget ids. You can get a list of interactions from multiple widgets of the same `kind` by passing multiple ids.

```graphql
mutation WidgetInteractions {
  widgetsInteractions(input: {id: TEXT_POLL, ids: $ids}, profileId: $profileId) {
    interactions {
      id
      optionId
      widgetId
      profileId
      createdAt
    }
}
```

> 👍 View the [Sample Repo](https://github.com/LiveLike/react-graphql-examples) to see everything put together.