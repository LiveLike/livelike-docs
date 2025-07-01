---
title: Status Tier
deprecated: false
hidden: true
metadata:
  robots: index
---
The **Status Tier** feature enables the creation of tiered reward systems where users unlock benefits based on activity or rewards. Tiers are organized into groups, with optional reward thresholds for automatic progression.

## Key Components

### 1. Tier Group

* **Purpose**: A container for related tiers (e.g., "Loyalty Program").
* **Fields**:
  * `Name` (e.g., "VIP Levels")
  * `Description` (optional)
  * `Visibility` (public/private)

### 2. Tier

* **Hierarchy**: Levels within a group (e.g., Bronze → Silver → Gold).
* **Configuration**:
  * `Reward Threshold` (optional): Auto-assign tier when users hit this value.
  * `Manual Assignment`: No threshold (admins assign manually).
  * `Priority`: Defines unlock order.

### 3. Benefits

* **Perks**: Attached to tiers (e.g., discounts, early access).
* **Types**: Static (fixed) or dynamic (conditional).