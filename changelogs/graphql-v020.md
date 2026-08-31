---
title: GraphQL v0.2.0
author: Jordanco Trpcevski
hidden: false
published_at: '2024-04-15T07:06:26.085Z'
---
## Changes Summary

Based on the GraphQL schema, here are the release changes. This schema introduces a variety of types, inputs, interfaces, and enums designed to enhance the GraphQL API's capabilities, particularly focusing on programs and poll updates. Below is a structured documentation to outline these changes:

***

### Release Changes

#### Program

***

* **program**: Get a specific program by ID.
* **programByCustomId**: Get a specific program by Custom ID.
* **programs**: Get a list of programs.
* **createProgram**: Create a new program by ID or Custom ID.
* **updateProgram**: Update existing program by ID.
* **updateProgramByCustomId**: Update existing program by Custom ID.
* **deleteProgram**: Delete existing program by ID.
* **deleteProgramByCustomId**: Delete existing program by Custom ID.

#### Poll

***

* **textPoll**: Get a specific poll by ID.