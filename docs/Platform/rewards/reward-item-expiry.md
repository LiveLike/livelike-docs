---
title: Reward Item Expiry
excerpt: >-
  Reward Item Expiry defines how long points earned through a reward item remain
  valid, allowing operators to configure different expiration policies for
  different point currencies.
deprecated: false
hidden: true
metadata:
  robots: index
---
Reward Item Expiry lets you put a time limit on the points your users earn, so balances stay fresh, liability doesn't quietly pile up on your books, and users always know where they stand. Expiry is configured **per reward item**, which matters because most programs run more than one point currency in parallel: redeemable points that get spent in a rewards store, and member or tier points that just accumulate toward status. These two don't behave the same way, so they shouldn't be forced onto the same expiry policy.

A well-tuned expiry policy does real work for your program:

- **Drives re-engagement** by creating natural urgency around point balances between events
- **Reduces long-term points liability** sitting on your balance sheet
- **Lets redeemable and status-based currencies run on different lifecycles** within the same deployment
- **Keeps users informed** — they always know how many points are at risk and when

LiveLike supports two ways to configure expiry, based on how points are tracked and voided:

| Type                         | How It Works                                                                                                                                            | Best For                                                                                     |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Earn-Based Expiry Period** | Every earn gets its own expiry — a fixed number of days from when it was earned. When a user spends points, the ones closest to expiring are used first | Redeemable points that users accumulate and spend over time                                  |
| **Global Expiry Date**       | All points earned into the reward item expire together, on one date you configure                                                                       | Tier or member points that reset on a recurring calendar (e.g. a season) and are never spent |

You can also leave expiry **off** for any reward item, which keeps today's behavior — points that never expire.

***

## Expiry Types

### Earn-Based Expiry Period

With Earn-Based Expiry Period, every earn is tracked individually and expires on its own schedule — a fixed window of days from the date it was earned. Rather than one lump balance, points are held in small groups ("buckets") behind the scenes. The upside for your users: they lose small amounts over time instead of losing everything at once, and can see exactly how much is expiring and when.

**Key configuration fields:**

| Field              | Description                                                            |
| ------------------ | ---------------------------------------------------------------------- |
| `expiry_mode`      | Set to `fifo`                                                          |
| `fifo_window_days` | Number of days from the earn date to expiry. Minimum 1 day, no maximum |

**How spending works:** when a user redeems, points are drawn from the bucket closest to expiring first, moving on to the next bucket if needed to cover the full amount. If a bucket is only partly spent, whatever's left keeps its original expiry — spending never resets the clock on remaining points.

**A note on same-day earns:** if a user earns points into the same reward item more than once on the same calendar day, those earns are grouped together since they'll expire on the same date anyway. "Same day" is based on your deployment's configured timezone, so it's worth setting this deliberately — an operator running in India, for instance, should set it to `Asia/Kolkata` to avoid awkward midnight boundary effects.

**Example: Redeemable points on a 30-day window**

Say you want points to stay "fresh" so users redeem regularly instead of stockpiling.

- You configure "Redeemable Points" with `expiry_mode: fifo` and `fifo_window_days: 30`
- A user earns 100 pts on Jun 1, 200 pts on Jun 5, and 700 pts on Jun 10 — creating three buckets that expire Jul 1, Jul 5, and Jul 10
- On Jun 29, the user redeems an 800-pt item. Buckets A and B (Jun 1 and Jun 5) are fully used up, and 500 of the 700 pts from Bucket C are used — leaving 200 pts still expiring Jul 10
- If the user hadn't redeemed anything, each bucket would simply expire on its own date, and each shows up as its own entry in their transaction history

### Global Expiry Date

With Global Expiry Date, you set one calendar date, and every point earned into that reward item — no matter when it was earned — expires on that date. There's no per-earn tracking here; everything lives in one pool that gets voided all at once when the date arrives.

**Key configuration fields:**

| Field                    | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| `expiry_mode`            | Set to `fixed-date`                                     |
| `fixed-date_expiry_date` | The date the balance expires. Must be set in the future |

**Example: Season-based tier points**

Say you want member or tier points to reset cleanly at the end of a season, rather than dribbling away individually.

- You configure "Member Points" with `expiry_mode: fixed-date` and `fixed-date_expiry_date: Aug 31`
- A user earns 50 pts on Jun 1, 75 pts on Jun 18, and 100 pts on Jul 4 — all three earns are tagged to expire Aug 31
- On Aug 31, the user's full 225-pt balance is voided in a single expiry event
- If you set a new expiry date for the following season, new earns pick up that date automatically — the prior balance has already been cleared

> Since this kind of reward item is typically never spent, there's no "which points get used first" logic to think about — the whole pool simply comes and goes together.

### No Expiry

Setting `expiry_mode` to `none` keeps things exactly as they are today: points never expire, no expiry schedule is shown to the user, and the balance behaves as a simple running total.

***

## How Spending, Balances, and Refunds Work

**Spending (debits):**

- If a user doesn't have enough available balance, the redemption is rejected.
- Under Earn-Based Expiry Period, points are drawn oldest-expiry-first, and the system keeps a record of exactly how much came from which bucket — this is what powers the "points used" breakdown shown to users.
- Under Global Expiry Date, points simply come out of the single pool.
- Expired points are never spendable, whether or not the cleanup process has gotten around to formally marking them yet.

**Balance accuracy:** a user's balance always excludes points that have expired, based on the expiry date itself — not on whether a background job has processed it yet. That background job exists to keep transaction history tidy; it's never the thing standing between a user and an accurate, up-to-date balance. History entries may lag by up to a day, but balances never do.

**Refunds:** when a redemption is reversed, the refunded points always come back as a **brand-new bucket** with its own expiry — they're never restored into the bucket they originally came from. This keeps refunds simple and sidesteps any confusion about whether the original bucket had already expired.

- You can specify a custom expiry for a refund if you want one.
- If you don't, it defaults to whatever the reward item's current expiry configuration would produce, starting from the refund date.
- Under Global Expiry Date, refunded points just rejoin the single pool and follow its existing expiry date.

**Example:** A user redeems 250 pts on Jun 28 under a 30-day Earn-Based window — using up all 100 pts from a bucket expiring Jul 1, and 150 of 200 pts from a bucket expiring Jul 5. The redemption gets refunded on Jul 3. The 250 pts come back as one new bucket, expiring Aug 2 (30 days from the refund), regardless of what had happened to the original buckets in the meantime.

***

## What Your Users See

- **Balance screen:** their total available points up front, with an expiry schedule underneath listing "\[X pts] expire on \[date]," soonest first. Under Global Expiry Date, this is just one line. If expiry is off, there's no schedule at all — just the balance.
- **Redemption confirmation & history:** under Earn-Based Expiry Period, users see exactly which points were spent — e.g. "Points used: 100 pts expiring Jul 1, 200 pts expiring Jul 5." Under Global Expiry Date, no breakdown is needed since there's only one pool.
- **Passive expiry:** shows up in transaction history as "\[X pts] expired on \[date]." If several buckets expire on the same day, each appears as its own line; a Global Expiry Date voiding appears as a single event.
- **Notifications:** LiveLike doesn't send expiry reminders directly. Instead, we fire a webhook ahead of an upcoming expiry, so you can build the notification experience that fits your product — your channel, your timing, your copy.

***

## Setting Up

### Via CMS

1. Open the reward item's creation or edit screen
2. Under **Expiry**, choose **No Expiry**, **Earn-Based Expiry Period**, or **Global Expiry Date**
3. _(Earn-Based only)_ Enter the expiry window, in days
4. _(Global Expiry Date only)_ Set the expiry date — it needs to be in the future
5. Save

> Expiry mode is locked in once set. If you need a different lifecycle later, that means setting up a new reward item rather than switching an existing one.

### Via API

Expiry configuration is added to the existing reward item create/update calls — there's no separate endpoint to learn. Pass `expiry_mode` (`none` · `fifo` · `fixed-date`) along with `fifo_window_days` or `fixed-date_expiry_date`, depending on the mode.

***

## Managing Expiry Over Time

**Editing settings:** you can update a reward item's expiry configuration whenever you like, but changes only apply to points earned **after** the change — existing balances keep the expiry they were originally given. Worth keeping in mind: adjusting the window or date won't retroactively shift when a user's current points expire.

**Tracking liability:** you can pull the outstanding balance for a reward item grouped by upcoming expiry date, filterable by reward item and date, so you can see how much liability is coming off the books and when — updated in near real time.

***

## Frequently Asked Questions

### Setup

**Can I combine Earn-Based Expiry Period and Global Expiry Date on the same reward item?**
No — each reward item runs one expiry mode at a time. If you need both behaviors, that's two reward items.

**Is there a limit to how long an Earn-Based window can be?**
Not currently — you can set any window of 1 day or more. We're evaluating whether a cap makes sense here, so this may evolve.

**Can I switch a reward item between Earn-Based and Global Expiry Date after it's live?**
No, mode changes aren't supported on an existing reward item. You'd set up a new one instead.

### Earning and Spending

**If a redemption only partly uses up a bucket, does the leftover get a new expiry?**
No — whatever's left keeps its original expiry date. Spending never resets the clock.

**What happens if a user tries to redeem twice at once and doesn't have enough for both?**
One redemption succeeds, the other is rejected with an insufficient-balance error. Users can never spend more than their available balance, even under simultaneous requests.

**Do users see stale balances if the cleanup job hasn't run yet?**
No — balances are always accurate based on the expiry date itself. The cleanup job only affects when history entries get written (within about 24 hours), never what the user sees as available to spend.

### Refunds

**Do refunded points go back to the bucket they came from?**
No — every refund creates a fresh bucket with a new expiry, even if the original bucket has since expired.

**Can I control the expiry on a refund?**
Yes, you can specify one. If you don't, it defaults to the reward item's current expiry rules, calculated from the refund date.

### Managing

**If I change the expiry window or date, does it affect points users already have?**
No — only points earned going forward are affected. Existing balances keep the expiry they started with.

**Can I turn on expiry for a reward item that already has a balance?**
Yes, though we'd recommend giving users a heads-up before you do — once enabled, existing balances are typically treated as freshly earned as of the rollout date under the new rule.

**How do I see what's about to expire across my user base?**
Use the liability view, grouped by expiry date and filterable by reward item, updated in near real time.

**Will LiveLike remind users before their points expire?**
Not directly — we send a webhook ahead of the expiry so you can trigger your own notification, in whatever channel and timing works for your product.
