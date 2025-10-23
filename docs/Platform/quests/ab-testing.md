---
title: A/B Testing
deprecated: false
hidden: true
metadata:
  robots: index
---
<br />

### Overview

The **A/B Testing** feature allows producers to create two variants of a single quest (Variant A and Variant B) to test different task setups, reward compositions, or difficulty levels.  
This helps identify which version drives higher user engagement or completion rates.

***

### Enabling A/B Testing

**Step 1: Basic Settings**

1. Toggle **Enable A/B Testing** ON.
2. Enter a **Test Name** and **Test Description** (mandatory when the toggle is enabled).
3. Provide **Variant A Name** and **Variant B Name**.
4. Continue to Objectives and Rewards steps to configure variant-specific elements.

> ⚠️ When A/B Testing is enabled, both variants must be fully configured before publishing.

***

### Configuring Variants

| **Step**                    | **Shared Fields**                                   | **Variant-Specific Fields**                |
| --------------------------- | --------------------------------------------------- | ------------------------------------------ |
| **Step 1 — Basic Settings** | Quest name, duration, user groups, quest attributes | —                                          |
| **Step 2 — Objectives**     | —                                                   | Tasks, task attributes, task target values |
| **Step 3 — Rewards**        | —                                                   | Rewards, badges, sponsors                  |

**Additional Notes**

* Configuring rewards is **optional**, but if a reward is added, it must include an **assigned amount**.
* There is **no cap** on the number of reward items per variant (one variant may have several, while the other may have none).

***

### Publishing A/B Quests

* The **Publish** button is available on the **Rewards** step.
* Both variants must pass all validation checks before publishing:
  * At least one task per variant.
  * Shared fields (quest name, duration, user group) are consistent across variants.
  * No duplicate task names within a quest or within variants.
  * Reward items, if added, must include assigned values.
* Once published:
  * Variants are **locked** and cannot be edited or deleted.
  * The parent quest status changes to **Published**.

***

### User Assignment & Tracking

* Users are **randomly and evenly assigned** to Variant A or Variant B the first time they encounter the quest.
* Assignment is handled server-side and remains consistent for the user.
* Key metrics per variant are automatically tracked for performance comparison.

***

### Analytics (Coming Soon)

Quest performance analytics will be available on the **Quest Details** page.

#### **Overview (Default View)**

Metrics shown for both A/B and non-A/B quests:

* Reached (Exposure): total user quests created
* Started: users who attempted ≥1 task
* Completed: users who finished all tasks
* Reward Claimed: users who claimed rewards (if applicable)
* Funnel Graph: Reached → Started → Completed → Claimed

#### **Engagement (Expanded View)**

**When A/B Testing is disabled:**

* Conversion Rate: Started ÷ Reached
* Completion Rate: Completed ÷ Started
* Reward Claim Rate: Claimed ÷ Completed
* Avg Time-to-Completion: created_at → completed_at

**When A/B Testing is enabled:**  
Displayed **side-by-side per variant**

* Users Assigned (distribution check)
* Conversion Rate per variant
* Completion Rate per variant
* Reward Claim Rate per variant
* Avg Time-to-Completion comparison
* Funnel comparison (A vs B)
* Highlight: “Current Leader: Variant X with Y% Completion”

> Some analytics are tracked by default and are **configurable per client**.  
> Data will be fetched through upcoming **Analytics APIs** to display dynamic dashboards.

***

### Benefits

**Data-driven insights** – Understand what setup drives engagement  
**Easy experimentation** – Test without duplicating quests  
**Automatic tracking** – System handles random assignment and logging  
**Continuous optimization** – Improve quest performance over time
