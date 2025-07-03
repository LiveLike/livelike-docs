---
title: Rewards Table Capping
deprecated: false
hidden: false
metadata:
  robots: index
---
# Reward Capping Product Guide

Last updated: May 2025  
Owner: Rewards & Loyalty Pod

---

## Overview

Reward Capping provides producers with greater control over the distribution of rewards by introducing two independent mechanisms:

1. **Reward Limit** – Cap the total number of times a user can earn a reward in a defined time period.
2. **Rate Limit** – Enforce a minimum time interval between earning rewards for an action.

These mechanisms are modular: they can be configured individually or together for the same reward rule to prevent abuse, manage reward inflation, and create fair, engaging user experiences.

---

## Objective

Enable producers to:

- Limit how many times a user can earn rewards for an action in a day or month.
- Control how frequently rewards can be earned (e.g. once every 10 minutes).
- Combine both caps for granular control over rewards distribution.

---

## Cap Mechanisms

### 1. Reward Limit

**What it does:**  
Caps the total number of rewards a user can earn for an action within a specified window (e.g. per day or per month).

**Example:**  
Users can earn rewards for watching VODs up to a max of 3 times per day.

**CMS Configuration Fields:**

- Enable Reward Limit: Toggle to turn it on/off.
- Time Window Type: Dropdown for Calendar Day or Calendar Month.
- Timezone: Dropdown to select timezone for Calendar windows.
- Max Rewardable Actions: Integer field (e.g. 3).

---

### 2. Rate Limit

**What it does:**  
Enforces a minimum time gap between rewarded actions for the same user.

**Example:**  
Users can only earn a reward for watching VODs once every 10 minutes.

**CMS Configuration Fields:**

- Enable Rate Limit: Toggle to turn it on/off.
- Cooldown Interval: Numeric input + unit selector (e.g. 10 minutes).

---

## Backend Logic Summary

| Mechanism | Logic Flow |
|-----------|------------|
| Reward Limit | - Convert current timestamp to configured timezone. Then calculate start and end of day/month window. Count rewards earned by user for this action in the window. If count is equal to or exceeds the limit, reject reward. |
| Rate Limit | - Retrieve last rewarded timestamp for the user/action. Calculate time difference from now. If less than cooldown interval, reject reward. |

Both evaluations run independently and modularly at runtime. If both are configured, both must pass for reward issuance.

---

## Example Configurations

| Scenario | Reward Limit | Rate Limit |
|----------|--------------|------------|
| Max 3 rewards per day | Yes | No |
| Reward only once every 10 mins | No | Yes |
| Max 5 per day, 1 every 5 mins | Yes | Yes |

---

## CMS Implementation

### Reward Table Entry Form Updates

- Two independent toggles:
  - Enable Reward Limit
  - Enable Rate Limit
- Dynamic form fields shown based on toggle state.
- Producers can configure either cap alone, or both together.
- Validation ensures required fields are filled when enabled.

### Reward Table Display

- New columns added:
  - Capping Type: Reward Limit / Rate Limit / Both / No Cap.
  - Max Rewardable Actions: Displays configured value or “Not Applicable”.
  - Time Period: For example, per day (EST), every 10 mins, or “Not Applicable”.

---

## API Changes

- create_reward_table_entry
  - Accepts an optional reward_capping object with:
    - reward_limit: unit (day/month), timezone (string), max_count (int)
    - rate_limit: duration (int), unit (min/hour)
- get_reward_table_entries
  - Returns the configured capping fields if present.

---

## Logging & Debugging

A new InvokedActionRewardLog is introduced to:

- Record every evaluated reward action and its outcome.
- Include reasons if reward is rejected (e.g. Reward limit reached, Rate limit not satisfied).
- Enable transparency for support, debugging, and analytics.

---

## Constraints & Assumptions

- Applies only to rewardable actions created after rollout.
- All timestamps stored in UTC, adjusted per configured timezone.
- Reward Limit currently supports Calendar Day and Calendar Month windows only.
- Rate Limit supports cooldowns in minutes, hours, or days.

---

## Known Challenges

- Concurrency: Multiple requests processed simultaneously may bypass limits if not handled atomically.

---

## Summary

Reward Capping gives producers powerful, modular tools to control reward distribution effectively. It ensures:

- Fairness and strategic behavior shaping.
- Prevention of reward farming abuse.
- Flexible configurations with minimal complexity.