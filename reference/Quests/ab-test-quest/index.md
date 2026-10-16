---
title: A/B Test Quest
deprecated: false
hidden: false
metadata:
  robots: index
---
An A/B test quest is a quest with exactly two variants. Each variant has its own tasks, rewards, badges and sponsors, and every profile is assigned to one variant (50/50 split).

**Endpoints**

- [Create A/B Test Quest](ref:create-ab-test-quest) creates the quest, the A/B test and both variants in one call.
- [List A/B Test Quests](ref:list-ab-test-quests) lists the A/B test quests of an application.
- [Assign Quest Variants to Profile](ref:assign-quest-variant-to-profile) assigns (or returns the existing) variant of one or more A/B test quests for a profile.

**How the assignment works**

- `assignment_strategy` controls how profiles are split: `random` (default) or `round_robin`.
- A profile keeps the variant it is assigned the first time; later calls return the same variant.
- With `pre_assign_enabled`, every profile in the quest's profile groups gets a variant in the background when the quest is published. Otherwise a profile gets its variant on first request.

**A/B fields on other quest endpoints**

- Quests include `ab_test` (null for regular quests).
- Quest tasks accept `test_variant_id` to attach a task to a variant.
- Quest rewards include `test_variants`.
- User quests include `assigned_test_variant`, the variant the profile is in.
