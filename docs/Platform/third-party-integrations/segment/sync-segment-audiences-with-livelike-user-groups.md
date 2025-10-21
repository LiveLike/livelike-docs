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

   <Image align="center" border={false} src="https://files.readme.io/1eb65e9769b77bff449af608b5a4568544f90628a103484ef805649b38625161-Screenshot_2025-10-17_at_12.53.03_PM.png" />

3. Connect your audience to LiveLike. Select the LiveLike destination inside Segment.

   <Image align="center" border={false} src="https://files.readme.io/83f6f3c3069f6d5810457b620180a8beecbcf5628e5160edb4a4fab424fb6cb8-image.png" />

4. Enable event tracking. Turn on event tracking for the LiveLike destination.

   <Image align="center" border={false} src="https://files.readme.io/b30d064cd1c8197374eddaed71c1c3c3ce62d3990c470055e681af3631cc9547-image_1.png" />

5. Choose how to match users. Pick identifiers such as custom ID, LiveLike profile ID, or nickname.

   <Image align="center" border={false} src="https://files.readme.io/6405fe3724a6a46bee65027a00fedb15f5abb59f8379777e0366adde3c528f76-image_2.png" />

6. Sync your group. Save your setup and select the action “Sync to User Group.”

   <Image align="center" border={false} src="https://files.readme.io/232856591ea3e761ad0250683eb70929ba9cc7768e0fadf801ddc4402c9c3189-image_3.png" />

That’s it! Your LiveLike group will now stay in sync with your Segment audience automatically.

## Best practices

For optimal setup and data consistency:

* Create your LiveLike group first,
* Sync it with the desired Segment Audience before adding any users manually.

This sequence ensures that group membership, IDs, and sync logic are aligned from the start, minimizing rework or data mismatches.

If you already have an existing audience that you want to backfill into a group, export the audience from Segment as CSV, and then import it into the group.

<br />
