---
title: Reward Item Expiry
excerpt: Defines how long rewards earned remain valid
deprecated: false
hidden: true
metadata:
  robots: index
---
Reward Item Expiry allows operators to configure how long points earned through a specific Reward Item remain valid. Instead of applying one expiry policy across all rewards, each Reward Item can define its own lifecycle.

Reward Item Expiry operates independently for each Reward Item and automatically affects point earning, redemption, refunds, balances, and transaction history.

***

LiveLike supports two ways to configure expiry:

| Type                                         | How It Works                                                                                                                                                                                                                                                 | Best  For                                                                             |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------- |
| **Earn-Based Expiry Period (in days)**       | Tracked at reward transaction level. Every reward credit transaction carries it's own validity (in days) calculated from the date of transaction. Users cannot redeem reward item earned in a single transaction post the expiry window of that transaction. | A usable currency that users accumulate and spend over time                           |
| **Global Expiry Date (fixed calendar date)** | Tracked at reward item level. Every users' entire balance expires on a fixed calendar date. Users cannot earn or redeem that reward item post the expiry.                                                                                                    | A status-based currency that resets on a recurring calendar (e.g. a season end date). |

If both are set on the same reward item, whichever comes first wins for any given earn: the Earn-Based window, or the Global Expiry Date. **Expiry always happens end of day in UTC timezone**.

You can also leave both off for any reward item — balances never expires.

***

## Expiry Types

### Earn-Based Expiry Period

With Earn-Based Expiry Period, every transaction is tracked individually and expires on its own schedule, a fixed window (in calendar days) calculated from the date of each transaction. Rather than one lump balance, earns are held in small groups ("buckets") behind the scenes. The upside for your users: they lose small amounts over time instead of losing everything at once, and can see exactly how much is expiring and when.

#### Key configuration fields:<br />

| Field              | Description                                                                                                          |
| ------------------ | -------------------------------------------------------------------------------------------------------------------- |
| `expiry_mode`      | Set to `fifo` - first in first out.                                                                                  |
| fifo\_window\_days | Number of days from the earn date to expiry. Minimum 1 day, no maximum. Set this to turn Earn-Based Expiry Period on |

**How spending works:** when a user redeems, points are drawn from the bucket closest to expiring first, moving on to the next bucket if needed to cover the full amount. If a bucket is only partly spent, whatever's left keeps its original expiry - spending never resets the clock on remaining points.

**A note on same-day earns:** if a user earns points into the same reward item more than once on the same calendar day, those earns are grouped together since they'll expire on the same date anyway. Calendar day is based on UTC timezone. It cannot be changed.

**Example: Redeemable points on a 30-day window**

Say you want points to stay "fresh" so users redeem regularly instead of stockpiling.

- You configure reward item as "Redeemable Points" with `expiry_mode: fifo` and `fifo_window_days: 30`
- A user earns 100 pts on Jun 1, 200 pts on Jun 5, and 700 pts on Jun 10 - creating three buckets that expire end of day (UTC) on Jul 1, Jul 5, and Jul 10 respectively.
- On Jun 29, the user redeems an 800-pt item. Buckets A and B (Jun 1 and Jun 5) are fully used up, and 500 of the 700 pts from Bucket C are used, leaving 200 pts still expiring end of day on Jul 10
- If the user hadn't redeemed anything, each bucket would simply expire on its own date, and each shows up as its own entry in their transaction history

### Global Expiry Date

With Global Expiry Date, you set one calendar date, and every point earned into that reward item - no matter when it was earned, expires on that date for all users simultaneously. There's no per-earn tracking here; everything lives in one pool that gets voided all at once when the date arrives. Both earning and redmeption is restricted post expiry

**Key configuration fields:**

| Field                    | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| `expiry_mode`            | Set to `fixed-date`                                     |
| `fixed-date_expiry_date` | The date the balance expires. Must be set in the future |

**Example: Season-based tier points**

Say you want member or tier points to reset cleanly at the end of a season, rather than dribbling away individually.

- You configure "Tier Points" with `expiry_mode: fixed-date` and `fixed-date_expiry_date: Aug 31`
- A user earns 50 pts on Jun 1, 75 pts on Jun 18, and 100 pts on Jul 4 - all three earns are tagged to expire Aug 31
- On Aug 31, the user's full 225-pt balance is voided in a single expiry event
- If you set a new expiry date, entire pool of that reward item (earned in past as well as in future) picks up that date automatically

> Since this kind of reward item is typically never spent, there's no "which points get used first" logic to think about, the whole pool simply goes out together.

### No Expiry

Setting `expiry_mode` to `none` keeps things exactly as they are today: points never expire, no expiry schedule is shown to the user, and the balance behaves as a simple running total.&#x20;

***

## Reward Item Sources Supported

Reward Item Expiry applies to all sources of earning such as Manual Credits, Streaks Milestones, Quest Rewards, Widgets, and Reward Table. Any points awarded follow the expiry configuration of the associated reward item, ensuring a consistent experience across.

***

## How Spending, Balances, and Refunds Work

**Spending (debits):**

- Under Earn-Based Expiry Period, points are drawn nearest-to-expiry-first, and the system keeps a record of exactly how much came from which bucket - this is what powers the "points used" breakdown shown to users.
- Under Global Expiry Date, points simply come out of the single pool.
- Expired points are never spendable.

**Balance accuracy:** a user's balance always excludes points that have expired, based on the expiry date itself - not on whether a background job has processed it yet. That background job exists to keep transaction history tidy; it's never the thing standing between a user and an accurate, up-to-date balance. History entries may lag by up to a day, but balances never do.

**Refunds:** when a redemption is reversed, the refunded points always come back as a **brand-new bucket** with its own expiry - they're never restored into the bucket they originally came from. This keeps refunds simple and sidesteps any confusion about whether the original bucket had already expired.

- You can specify a new expiry window for a refund if you want one.
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

**Tracking liability:** you can pull the outstanding balance for a reward item grouped by upcoming expiry date, filterable by reward item and date, so you can see how much liability is coming off the books and when — updated in near real time.

***

## Frequently Asked Questions

### Setup

**Can I combine Earn-Based Expiry Period and Global Expiry Date on the same reward item?**<br />Yes - when a reward item has both modes enabled, the global expiry date take priority.&#x20;

**Is there a limit to how long an Earn-Based window can be?**<br />No - you can set any window counted in days - 1 or more.

**Can I enable either one of them later after the reward item is live?**<br />Yes - in case of earn-based expiry the effect is not retroactively applied - only new transactions / earning will be impacted. For global expiry, all reward items will take on the newly set expiry date.

**Can I disable expiry?**<br />Yes - in case of earn-based expiry the effect is not retroactively applied. Reward earned in previous transactions will expire when the window runs out. Global expiry is completely removed.&#x20;

### Earning and Spending

**If a redemption only partly uses up a bucket, does the leftover get a new expiry?**<br />No - whatever's left keeps its original expiry date. Spending never resets the clock.

**What happens if a user tries to redeem twice at once and doesn't have enough for both?**
One redemption succeeds, the other is rejected with an insufficient-balance error. Users can never spend more than their available balance, even under simultaneous requests.

**Do users see stale balances if the cleanup job hasn't run yet?**<br />No - balances are always accurate based on the expiry date itself. The cleanup job only affects when history entries get written (within about 24 hours), never what the user sees as available to spend.

### Managing

**If I change the earn-based expiry window, does it affect points users already have?**<br />No - only points earned going forward are affected. Existing balances keep the expiry they started with.

**If I change the global expiry date, does it affect points users already have?**<br />Yes - global date change updates expiry for the entire reward item for all users.

**Can I update global expiry date after the original date has passed?**<br />No - date change needs to happen before the global expiry date passes.

**How do I see what's about to expire across my user base?**
Use the liability view, grouped by expiry date and filterable by reward item, updated in near real time.

**Will LiveLike remind users before their points expire?**<br />You can configure a webhook to trigger your own notification, in whatever channel and timing works for your product.
