---
title: Sync Segment Audiences to LiveLike User Groups
deprecated: false
hidden: true
metadata:
  robots: index
---
Managing audiences across platforms doesn’t have to be a manual chore. Instead of adding and removing users one by one, you can now sync your Segment Audiences directly to LiveLike User Groups.
This ensures your LiveLike groups always stay up to date with the audiences you define in Segment—automatically.

## Why This Matters & Key Benefits

* Save time – No more manual updates, your groups always reflect the latest Segment audiences.
* Stay accurate – Direct sync ensures your Segment Audiences connect seamlessly with LiveLike User Groups, either at creation or later.
* Stay flexible – You can still add users manually, stop syncing anytime, and see at a glance which groups are synced.

## Handling Existing Members

When syncing a Segment Audience that already contains members, existing users can be imported into LiveLike via a CSV upload of either user_id or profile_id.

If an incoming user record does not contain a livelike_profile_id or custom_id, the system will automatically create a new profile:

* If a nickname is provided, it will be assigned to the new profile.
* If no nickname is provided, the system will generate a random nickname.

User records can be fetched and added using either:

* Profile ID
* Custom ID

This process ensures that groups are fully populated and up to date from the very first sync.

## How to Set It Up

Getting started is simple:

1. Create your audience in Segment
   Define who you want to target using events, traits, or existing data.

2. Connect your audience to LiveLike
   Select the LiveLike destination inside Segment.

   <Image align="center" src="https://files.readme.io/83f6f3c3069f6d5810457b620180a8beecbcf5628e5160edb4a4fab424fb6cb8-image.png" />

3. Enable event tracking
   Turn on event tracking for the LiveLike destination.

   <Image align="center" src="https://files.readme.io/b30d064cd1c8197374eddaed71c1c3c3ce62d3990c470055e681af3631cc9547-image_1.png" />

4. Choose how to match users
   Pick identifiers such as custom ID, LiveLike profile ID, or nickname.

   <Image align="center" src="https://files.readme.io/6405fe3724a6a46bee65027a00fedb15f5abb59f8379777e0366adde3c528f76-image_2.png" />

5. Sync your group
   Save your setup and select the action “Sync to User Group.”

   <Image align="center" src="https://files.readme.io/232856591ea3e761ad0250683eb70929ba9cc7768e0fadf801ddc4402c9c3189-image_3.png" />

That’s it — your Segment audience will now stay in sync with your LiveLike User Group automatically.

## Best Practice

For the smoothest setup:

* Create your LiveLike group first,
* Then sync it with a Segment Audience before adding users.

This ensures everything is aligned from the start.

With Segment–LiveLike syncing, you can stop worrying about audience management and focus on engaging your users where it matters most.
