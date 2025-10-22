---
title: Sync Segment Audiences to User Groups
deprecated: false
hidden: true
metadata:
  robots: index
---
Segment Audiences can be kept in sync with User Groups on LiveLike. This ensures groups on LiveLike always stay up to date with their corresponding audiences you define in Segment.

## Why sync audiences to groups

* Save time. No need to update LiveLike and Segment separately.
* Stay accurate. Syncing ensures your groups always reflect their corresponding Segment audiences.
* Keep flexibility. You can still add members manually, stop syncing anytime, and see at a glance which groups are synced.

## Mapping Segment users to profiles

Segment users can be mapped to LiveLike profiles via the `livelike_profile_id` or `custom_id` properties on the Segment user.

## Setting up group sync

1. Create your audience in Segment. Define who you want to target using events, traits, or existing data.

2. Create the corresponding group on LiveLike. Enable Segment Sync and configure the audience ID (starting with `aud_`) from Segment.

3. Connect your audience to LiveLike. Select the LiveLike destination inside Segment. 

   <Image align="center" border={false} src="https://files.readme.io/3f379b33ef084a6bf9ee994e9cf1549cbceba32681ba775696c89841319b30ea-Screenshot_2025-10-22_012337.png" />

   <Image align="center" border={false} src="https://files.readme.io/0064046fde1f6b1b6b1cde2915b507e6293d0a898fbd3de232c13cb13247c94d-Screenshot_2025-10-22_012416.png" />

4. Enable Track events for the destination. 

   <Image align="center" border={false} src="https://files.readme.io/128a2eec5503da86ee68c096e1a2ad65ec22d9c45ee7b291ead28960fb3811c4-Screenshot_2025-10-22_012456.png" />

5. Add identifiers you have setup for your audience using the customized setup. (These can include livelike_profile_id, custom_id, user_id, etc). 

   <Image align="center" border={false} src="https://files.readme.io/4c0778456b1f7db852ec4dc9701413aaa1f71f9ff30ccffc5318783a6ca13319-Screenshot_2025-10-22_012535.png" />

That’s it! Your LiveLike group will now stay in sync with your Segment audience automatically.

## Best practices

For optimal setup and data consistency:

* Create your LiveLike group first,
* Sync it with the desired Segment Audience before adding any users manually.

This sequence ensures that group membership, IDs, and sync logic are aligned from the start, minimizing rework or data mismatches.

If you already have an existing audience that you want to backfill into a group, export the audience from Segment as CSV, and then import it into the group.

<br />
