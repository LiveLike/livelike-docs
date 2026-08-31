---
title: GraphQL v0.1.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-04-04T09:03:43.000Z'
---
## Changes Summary

This release introduces a robust framework for managing user profiles, conducting polls, customizing and interacting with widgets, managing reaction spaces and packs, as well as creating and managing rich posts and comment boards. It enables applications to create a dynamic and interactive user experience with custom data and structured content.

***

Based on the GraphQL schema, here's a draft for the release changes documentation. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on user profiles, polls, widgets, reaction spaces, user reactions, and rich posts. Below is a structured documentation to outline these changes:

***

### Release Changes Documentation

#### Scalars

***

* **UUID**: Represents Universally Unique Identifiers (UUIDs).
* **JWT**: Represents JSON Web Tokens (JWT) for authentication purposes.
* **URL**: Ensures values conform to the standard URL format as per RFC3986.
* **NonNegativeInt**: Represents integers that are 0 or greater.
* **PositiveInt**: Represents integers greater than 0.
* **NonEmptyString**: A string scalar that cannot be empty.
* **DateTime**: Represents a date-time string in UTC format, compliant with RFC 3339.

#### Interfaces

***

* **Node**: A generic interface for any type with an `id` field of type UUID.
* **Edge**: Represents a connection edge with a `node` and a `cursor`.
* **Connection**: Represents a paginated list of edges.

#### Types

***

##### Profile and Authentication

* **ProfileAuth**: Contains authentication details for a profile.
* **Profile**: Represents a user profile with various identifiers and metadata.

##### Polls

* **TextPollOption & ImagePollOption**: Define options for text and image polls, respectively.
* **TextPoll & ImagePoll**: Represent text and image polls, including their options, status, and related metadata.

##### Widgets

* **Widget**: A union type that includes TextPoll, ImagePoll, and RichPost.
* **WidgetConnection, WidgetEdge, WidgetOrder**: Support pagination and ordering for collections of widgets.

##### Reaction Spaces

* **ReactionPack, ReactionSpace, UserReaction**: Types related to customizing reactions within spaces, managing reaction packs, and tracking user reactions.

##### Comments and Posts

* **CommentBoard**: Represents a board for hosting user comments.
* **RichPost**: Represents a rich content post, such as HTML content.

#### Enumerations

***

* **OrderEnum**: Supports ascending (ASC) and descending (DESC) ordering.
* **ProgramStatusEnum, PollEnum, WidgetStatusEnum, WidgetKindEnum**: Define various statuses and kinds for programs, polls, and widgets.

#### Inputs

***

Inputs for creating, updating, and fetching data, such as ProfileCreateInput, ProfileUpdateInput, TextPollCreateInput, ImagePollCreateInput, ReactionSpaceCreateInput, etc.

#### Queries and Mutations

***

Defines a comprehensive list of queries and mutations for creating, updating, fetching, and deleting profiles, polls, widgets, reaction spaces, comments, and posts.

***