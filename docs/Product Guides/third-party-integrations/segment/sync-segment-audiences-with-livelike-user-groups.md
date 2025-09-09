---
title: Sync Segment Audiences to User Groups
deprecated: false
hidden: true
metadata:
  robots: index
---
Managing audiences across platforms doesn’t have to be a manual chore. Instead of adding and removing users one by one, you can now sync your Segment Audiences directly to LiveLike User Groups. This ensures your LiveLike groups always stay up to date with the audiences you define in Segment.

## Why sync audiences to groups

* Save time. No need to update LiveLike and Segment separately.
* Stay accurate. Syncing ensures your groups always reflect their corresponding Segment audiences.
* Keep flexibility. You can still add members manually, stop syncing anytime, and see at a glance which groups are synced.

## Handling existing audiences

Segment users can be mapped to LiveLike profiles via the `livelike_profile_id` or `custom_id` properties on the Segment user.

When syncing a Segment Audience that already contains members, existing users can be imported into LiveLike via a CSV upload of either user_id or profile_id.

If an incoming user record does not contain a livelike_profile_id or custom_id property, the system will automatically create a new profile.

* If a nickname is provided, it will be assigned to the new profile.
* If no nickname is provided, the system will generate a random nickname.

User records can be fetched and added using either:

* Profile ID
* Custom ID

This process ensures that groups are fully populated and up to date from the very first sync.

## Setting up group sync

Getting started is simple:

1. Create your audience in Segment. Define who you want to target using events, traits, or existing data.

2. Connect your audience to LiveLike. Select the LiveLike destination inside Segment.

   <Image align="center" src="https://files.readme.io/83f6f3c3069f6d5810457b620180a8beecbcf5628e5160edb4a4fab424fb6cb8-image.png" />

3. Enable event tracking. Turn on event tracking for the LiveLike destination.

   <Image align="center" src="https://files.readme.io/b30d064cd1c8197374eddaed71c1c3c3ce62d3990c470055e681af3631cc9547-image_1.png" />

4. Choose how to match users. Pick identifiers such as custom ID, LiveLike profile ID, or nickname.

   <Image align="center" src="https://files.readme.io/6405fe3724a6a46bee65027a00fedb15f5abb59f8379777e0366adde3c528f76-image_2.png" />

5. Sync your group. Save your setup and select the action “Sync to User Group.”

   <Image align="center" src="https://files.readme.io/232856591ea3e761ad0250683eb70929ba9cc7768e0fadf801ddc4402c9c3189-image_3.png" />

That’s it! Your LiveLike group will now stay in sync with your Segment audience automatically.

## Best practices

For optimal setup and data consistency:

* Create your LiveLike group first,
* Sync it with the desired Segment Audience before adding any users manually.

This sequence ensures that group membership, IDs, and sync logic are aligned from the start, minimizing rework or data mismatches. With Segment-LiveLike syncing in place, audience management becomes automated, allowing teams to focus on building engaging features rather than keeping their tools up to date.

<br />