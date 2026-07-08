---
title: Reward Item Expiry
excerpt: >-
  Defines how long reward earned through a reward item remain valid, allowing
  operators to configure different expirations for different rewards.
deprecated: false
hidden: true
metadata:
  robots: index
---
Reward Item Expiry allows operators to configure how long points earned through a specific Reward Item remain valid. Instead of applying one expiry policy across all rewards, each Reward Item can define its own lifecycle.

Reward Item Expiry operates independently for each Reward Item and automatically affects point earning, redemption, refunds, balances, and transaction history.

***

LiveLike supports three ways to configure expiry, based on how points are tracked and voided:

| Type                         | How It Works                                                                      | Best  For                                                                                             |
| ---------------------------- | --------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Earn-Based Expiry Period** | Lets you decide how long users can keep reward after they are earned              | A redeemable currency that users accumulate and spend over time                                       |
| **Global Expiry Date**       | All reward earned into the reward item expire together, on one date you configure | A tier or member currency that resets on a recurring calendar (e.g. a season), or as a hard backstop. |

If both are set on the same reward item, whichever comes first wins for any given earn: the Earn-Based window, or the Global Expiry Date.

You can also leave both off for any reward item, which keeps today's behavior — balances that never expire.

***

## Expiry Types

### Earn-Based Expiry Period

With Earn-Based Expiry Period, every earn is tracked individually and expires on its own schedule, a fixed window of days from the date it was earned. Rather than one lump balance, earns are held in small groups ("buckets") behind the scenes. The upside for your users: they lose small amounts over time instead of losing everything at once, and can see exactly how much is expiring and when.

#### Key configuration fields:<br />

| Field              | Description                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `expiry_mode`      | Set to `fifo`                                                                                                        |
| fifo\_window\_days | Number of days from the earn date to expiry. Minimum 1 day, no maximum. Set this to turn Earn-Based Expiry Period on |

**How spending works:** when a user redeems, points are drawn from the bucket closest to expiring first, moving on to the next bucket if needed to cover the full amount. If a bucket is only partly spent, whatever's left keeps its original expiry - spending never resets the clock on remaining points.

**A note on same-day earns:** if a user earns points into the same reward item more than once on the same calendar day, those earns are grouped together since they'll expire on the same date anyway. "Same day" is based on your deployment's configured timezone, so it's worth setting this deliberately — an operator running in India, for instance, should set it to `Asia/Kolkata` to avoid awkward midnight boundary effects.

**Example: Redeemable points on a 30-day window**

Say you want points to stay "fresh" so users redeem regularly instead of stockpiling.

- You configure "Redeemable Points" with `expiry_mode: fifo` and `fifo_window_days: 30`
- A user earns 100 pts on Jun 1, 200 pts on Jun 5, and 700 pts on Jun 10 - creating three buckets that expire Jul 1, Jul 5, and Jul 10
- On Jun 29, the user redeems an 800-pt item. Buckets A and B (Jun 1 and Jun 5) are fully used up, and 500 of the 700 pts from Bucket C are used, leaving 200 pts still expiring Jul 10
- If the user hadn't redeemed anything, each bucket would simply expire on its own date, and each shows up as its own entry in their transaction history

### Global Expiry Date

With Global Expiry Date, you set one calendar date, and every point earned into that reward item - no matter when it was earned, expires on that date. There's no per-earn tracking here; everything lives in one pool that gets voided all at once when the date arrives.

**Key configuration fields:**

| Field                    | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| `expiry_mode`            | Set to `fixed-date`                                     |
| `fixed-date_expiry_date` | The date the balance expires. Must be set in the future |

**Example: Season-based tier points**

Say you want member or tier points to reset cleanly at the end of a season, rather than dribbling away individually.

- You configure "Member Points" with `expiry_mode: fixed-date` and `fixed-date_expiry_date: Aug 31`
- A user earns 50 pts on Jun 1, 75 pts on Jun 18, and 100 pts on Jul 4 - all three earns are tagged to expire Aug 31
- On Aug 31, the user's full 225-pt balance is voided in a single expiry event
- If you set a new expiry date for the following season, new earns pick up that date automatically, the prior balance has already been cleared

> Since this kind of reward item is typically never spent, there's no "which points get used first" logic to think about, the whole pool simply comes and goes together.

### No Expiry

Setting `expiry_mode` to `none` keeps things exactly as they are today: points never expire, no expiry schedule is shown to the user, and the balance behaves as a simple running total.

***

## Reward Types Supported

Reward Item Expiry applies to points earned through Badges, Streaks, and Quest rewards. Any points awarded from these experiences follow the expiry configuration of the associated reward item, ensuring a consistent experience across all reward types.

***

## How Spending, Balances, and Refunds Work

**Spending (debits):**

- If a user doesn't have enough available balance, the redemption is rejected.
- Under Earn-Based Expiry Period, points are drawn oldest-expiry-first, and the system keeps a record of exactly how much came from which bucket - this is what powers the "points used" breakdown shown to users.
- Under Global Expiry Date, points simply come out of the single pool.
- Expired points are never spendable, whether or not the cleanup process has gotten around to formally marking them yet.

**Balance accuracy:** a user's balance always excludes points that have expired, based on the expiry date itself - not on whether a background job has processed it yet. That background job exists to keep transaction history tidy; it's never the thing standing between a user and an accurate, up-to-date balance. History entries may lag by up to a day, but balances never do.

**Refunds:** when a redemption is reversed, the refunded points always come back as a **brand-new bucket** with its own expiry - they're never restored into the bucket they originally came from. This keeps refunds simple and sidesteps any confusion about whether the original bucket had already expired.

- You can specify a custom expiry for a refund if you want one.
- If you don't, it defaults to whatever the reward item's current expiry configuration would produce, starting from the refund date.
- Under Global Expiry Date, refunded points just rejoin the single pool and follow its existing expiry date.

**Example:** A user redeems 250 pts on Jun 28 under a 30-day Earn-Based window — using up all 100 pts from a bucket expiring Jul 1, and 150 of 200 pts from a bucket expiring Jul 5. The redemption gets refunded on Jul 3. The 250 pts come back as one new bucket, expiring Aug 2 (30 days from the refund), regardless of what had happened to the original buckets in the meantime.

***

## Setting Up Via CMS

1. Navigate to **Reward → Create New Reward Item**
2. Set a **Name** and optional **Description**
3. Under Reward Item Expiry, Turning this **toggle On** enables reward item to auto-expire based on the expiry configurations set. You can modify after the changes., Earn-Based Expiry Period, or Global Expiry Date
4. _(Earn-Based only)_ Enter the expiry window, in days
5. _(Global Expiry Date only)_ Set the expiry date - it needs to be in the future
6. Save

> If both are set, whichever comes first for a given earn - the Earn-Based window or the Global Expiry Date - is what determines when it expires.

***

## Managing Expiry Over Time

**Editing settings:** you can update a reward item's expiry configuration whenever you like, but changes only apply to points earned after the change - existing balances keep the expiry they were originally given. Worth keeping in mind: adjusting the window or date won't retroactively shift when a user's current points expire.

### Editing a Expiry (CMS)

- Navigate to **Reward**

- Locate the Reward and click **Edit**

- Update the desired fields

- Save

In **Draft** status can be fully edited, all configuration fields are modifiable before publication.

**Tracking liability:** you can pull the outstanding balance for a reward item grouped by upcoming expiry date, filterable by reward item and date, so you can see how much liability is coming off the books and when — updated in near real time.

***

## Frequently Asked Questions

### Setup

**Can I combine Earn-Based Expiry Period and Global Expiry Date on the same reward item?**<br />Yes - each reward item runs one expiry mode at a time. If you need both behaviors, that's two reward items.

**Is there a limit to how long an Earn-Based window can be?**<br />Not currently - you can set any window of 1 day or more. We're evaluating whether a cap makes sense here, so this may evolve.

**Can I switch a reward item between Earn-Based and Global Expiry Date after it's live?**
No, mode changes aren't supported on an existing reward item. You'd set up a new one instead.

**Can I disable expiry?**<br />Yes. Selecting No Expiry keeps points indefinitely.

### Earning and Spending

**If a redemption only partly uses up a bucket, does the leftover get a new expiry?**<br />No - whatever's left keeps its original expiry date. Spending never resets the clock.

**What happens if a user tries to redeem twice at once and doesn't have enough for both?**
One redemption succeeds, the other is rejected with an insufficient-balance error. Users can never spend more than their available balance, even under simultaneous requests.

**Do users see stale balances if the cleanup job hasn't run yet?**<br />No - balances are always accurate based on the expiry date itself. The cleanup job only affects when history entries get written (within about 24 hours), never what the user sees as available to spend.

### Managing

**If I change the expiry window or date, does it affect points users already have?**<br />No - only points earned going forward are affected. Existing balances keep the expiry they started with.

**Can I turn on expiry for a reward item that already has a balance?**<br />Yes, though we'd recommend giving users a heads-up before you do - once enabled, existing balances are typically treated as freshly earned as of the rollout date under the new rule.

**How do I see what's about to expire across my user base?**
Use the liability view, grouped by expiry date and filterable by reward item, updated in near real time.

**Will LiveLike remind users before their points expire?**<br />Not directly - we send a webhook ahead of the expiry so you can trigger your own notification, in whatever channel and timing works for your product.
