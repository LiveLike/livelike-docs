---
title: Flairs
excerpt: >-
  A universal and reusable label system that adds identity, status, and context
  to users, content, and experiences across the platform.
deprecated: false
hidden: false
metadata:
  robots: index
---
## What is Flair?

Flair is a universal labeling system used across the LiveLike platform to visually identify people, content, and experiences.

A flair is a small badge, tag, or visual marker that adds context and meaning. It can signal status, identity, achievement, verification, ownership, or special access. Flairs are designed to be lightweight, flexible, and reusable across different parts of the platform.

One flair definition can be used in many places and rendered consistently wherever it appears.

## What Flair Does

Flair helps users and systems quickly understand who someone is, what something represents, or why it matters, without needing extra explanation.

* **Identity and Status**
  * Flairs can represent roles and recognition such as VIP users, verified hosts, moderators, team members, or creators. This builds trust and clarity, especially in live and social environments.
* **Achievements and Progress**
  * Flairs can mark accomplishments like milestones, streaks, quest completion, or earned rewards. They give visible recognition and encourage repeat engagement.
* **Contextual Labels**
  * Flairs can label entities like chatrooms, quests, rewards, or events. Examples include difficulty levels, official status, rarity, or event-specific badges.
* **Personal Expression**
  * When allowed, users can select or create flairs to express themselves. These flairs appear consistently across supported surfaces such as profiles or chat.

## Where Flair Appears

Flairs are not tied to a single surface. The same system supports flairs on:

* User profiles and avatars
* Chatrooms, Comment Boards, Widgets, etc
* Quests, rewards, and achievements
* Teams, communities, and events

## Key Characteristics

* **Universal:** Works across users, content, and system entities.
* **Portable:** A single flair can be reused in multiple contexts.
* **Permission-aware:** Who can create, assign, or use flairs is controlled by rules.
* **Client-rendered:** Flair defines meaning and rules, not UI.

## Why Flair Matters

Flair creates a shared visual language across LiveLike. It increases clarity, trust, engagement, and emotional connection while enabling new surfaces for rewards, moderation, identity, and revenue.

## Flair Scopes

Flair Scopes define where a flair applies.
They represent a resource kind (e.g., chatroom, comment board, widget) and optionally a specific resource instance. Scopes can be created and updated from api and admin app.

Scopes are reusable and can be shared across multiple flair assignments.

Scopes can be global or specific.

#### Global vs Specific Scopes

* ##### Global scope
  resource_uuid = null → Applies to all resources of that kind in the application.
  **Example**: All chat rooms have the Official flair.
* ##### Specific scope
  resource_uuid = uuid → Applies only to the specific resource instance.
  **Example**: Chatroom 1234-abcd receives the Live Event flair.

## Flair Operations

Flairs are defined once and can then be assigned to supported resources based on permissions and rules.

Operations are supported in CMS and API:

* #### List Flairs
  Retrieves a paginated list of all flairs per application. <Anchor label="List Flairs Endpoint" target="_blank" href="https://docs.livelike.com/v1/reference/list-flairs">List Flairs Endpoint</Anchor>
* #### Create a Flair
  Creates a reusable flair definition that can later be assigned to users or resources. <Anchor label="Create Flair Endpoint" target="_blank" href="https://docs.livelike.com/v1/reference/create-a-flair">Create Flair Endpoint</Anchor>
* #### Update Flair
  Updates the metadata of an existing flair. <Anchor label="Update Flair Endpoint" target="_blank" href="https://docs.livelike.com/v1/reference/update-a-flair">Update Flair Endpoint</Anchor>
* #### Remove Flair
  Soft-deletes a flair. <Anchor label="Delete Flair" target="_blank" href="https://docs.livelike.com/v1/reference/delete-a-flair">Delete Flair</Anchor>
* #### Assign a Flair
  Assigns an existing flair to a supported resource. It must contain flair_id and one of profile_id or profile_custom_id and optionally scope_id.  If assignment contains scope_id flair will be assigned only for defined scope. Assignments are unique. Create assignment: <Anchor label="Assign Flair" target="_blank" href="https://docs.livelike.com/v1/create-a-flair-assignment">Assign Flair</Anchor>, list assignments <Anchor label="Assign Flair List" target="_blank" href="https://docs.livelike.com/v1/reference/list-flair-assignments">Assign Flair List</Anchor>
  * A flair assignment:
    * Links a flair definition to a user and/or resource
    * Can be manual (admin or moderator action) or automated (rules, achievements, events)
    * Does not duplicate the flair definition
    * Tracks who assigned it (assigned_by)
    * Can be activated or deactivated (Soft Delete)
* ##### Assignment:
  * Links a flair definition to a specific entity
  * Can be manual (admin/moderator action) or automated (rules, achievements, events)
  * Does not duplicate the flair definition
* ##### Examples:
  * Assign a VIP flair to a user
    * User has vip flair everywhere
  * Assign an Official flair to a chatroom
* #### Remove a Flair Assignment
  Removes an existing flair assignment from a resource. <Anchor label="Remove Assignment" target="_blank" href="https://docs.livelike.com/v1/reference/delete-a-flair-assignment">Remove Assignment</Anchor>
  * The flair definition remains intact
  * Only the association between the flair and the resource is removed
  * Can be triggered manually or automatically (e.g. expiration, rule violation)
* #### Update / Replace a Flair Assignment
  Updates the flair assignment on a resource. <Anchor label="Update Assignment" target="_blank" href="https://docs.livelike.com/v1/reference/update-a-flair-assignment">Update Assignment</Anchor>
  ##### Examples:
  * Replace one flair with another (e.g. Bronze → Silver)
  * Update assignment metadata (e.g. expiration date)
