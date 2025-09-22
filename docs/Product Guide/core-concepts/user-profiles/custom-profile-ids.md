---
title: Custom Profile IDs
deprecated: false
hidden: false
metadata:
  robots: index
---
<br />

Custom Profile IDs help integrations maintain a two-way mapping between their users and LiveLike profiles. Using custom IDs on profiles makes it so that you don't need to maintain your own mapping of user IDs to profile IDs, instead you supply your IDs as custom ID values and then use those values to look up profiles directly.

A <Glossary>Profile</Glossary> has two IDs:

* **<Glossary>Profile ID</Glossary>**: The profile ID is the unique identifier assigned by LiveLike when the profile is created. It can't be modified.
* **Custom ID**: The custom ID is optional and empty by default. It can be changed, but it has to be unique within the application.

## Looking Up Profiles by Custom ID

Use the [Get Profile by Custom ID](ref:get-profile-by-custom-id) endpoint to look up a profile by its custom ID.

## Creating Profiles with Custom IDs

There are two ways to create profiles with custom IDs: using [Client-generated Access Tokens](doc:client-generated-access-tokens) or the [Create Profile by Custom ID](ref:create-profile-by-custom-id) endpoint.

Requests authenticated with client-generated access tokens will implicitly create profiles the first time the custom ID is used, and subsequent requests with the same custom ID will authenticate as the same profile. When using client-generated access tokens a `custom_profile_id` claim must be included in the JWT. If a request using that JWT would implicitly create a profile, the `custom_profile_id` claim is used to set the custom ID on the new profile.

New profiles with custom IDs can be created via API call to the Create Profile by Custom ID endpoint. It is recommended to use the endpoint if you want requests to fail when the custom ID already exists. Requests to create a new profile will fail with a 409 status code when the custom ID is already in use:

```json
{
  "detail": "profile with custom_id 'example' already exists."
}
```
