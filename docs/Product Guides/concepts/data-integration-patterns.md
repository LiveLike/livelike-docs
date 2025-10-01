---
title: Data Integration Patterns
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
LiveLike provides a few ways to integrate your own data to make lookups and filtering easier, resulting in fewer API calls and less application-level logic. A few common patterns used across all of LiveLike's features are:

* Custom IDs: one-to-one mapping between entities in your system and LiveLike.
* Attributes: one-to-many mapping from your system to LiveLike.
* Custom data: supplementary data from your system memoized on LiveLike records.

## Custom IDs

Custom IDs are best used when there is a one-to-one mapping between entities in your system and LiveLike, such as  users to profiles, or content to programs. Custom IDs are unique within a resource and application, so two profiles in the same app can't have the same custom ID.

Some use cases for custom IDs are:

* Setting profile custom IDs to your user IDs. Read more on [Custom Profile IDs](doc:custom-profile-ids)
* Setting program custom IDs to your content IDs from your CMS, EPG, DAM, stats provider, etc.

## Attributes

Attributes are most useful for one-to-many mappings between entities in your system and LiveLike. Attributes are indexed on our side and can be queried via API, so you can return results matching the presence of a given attribute, or matching specific values.

Common use cases for custom IDs include:

* Finding all badges with a specific rarity
* Listing all programs belonging to a certain competition
* Querying for quests that are part of a given campaign

> 📘 Attribute size limits
>
> Attribute keys and values are limited to 200 characters each.

## Custom Data

Custom data is helpful for memoizing data from your system on relevant LiveLike records. That can reduce API call volume and limit the amount of joining or aggregation needed in your application logic.

> 🚧 Custom data can't be queried
>
> Prefer custom IDs or attributes if you want to query objects matching a given search. Custom data remains available for backward compatibility reasons, but generally you'll want to use custom IDs or attributes.

Typically, custom data is used for things like:

* Storing user preferences in a profile custom data
* Showing extra context in chat messages, like user roles or flair
