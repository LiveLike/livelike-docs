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

* A container for multiple tiers.
* Example: "VIP Levels", "Membership Tiers".

### 2. Tier

* A level within a group that contains benefits.
* Reward Threshold (Optional)
  * If set, users automatically qualify for the tier upon reaching the threshold.
  * Example: "Earn 1000 Dummy Dollars to unlock Gold Tier".
* Tier Order
  * Determines hierarchy within a group.
  * Auto-generated for tiers with reward thresholds (based on threshold value).
  * Manually adjustable for tiers without thresholds.
* Example: "Gold Tier", "Platinum Tier".

### 3. Benefits

* Perks or rewards associated with a tier.
* Multiple Benefits can be added within a Tier.
* Reward
  * A benefit can have a Reward linked.
  * If set user gets the reward on unlocking the Tier.
* Example: "Exclusive Discounts", "Early Access to Products".

<br />

## Managing Status Tier via CMS

### Accessing the Status Tier Feature

* Navigate to the "Status Tier" Tab
* Located on the left sidebar menu in the admin dashboard.
* Click to open the Status Tier management panel.

<br />

### Creating a Tier Group

#### Required Fields

* **Title (Mandatory)** → Name of the Tier Group (e.g., "VIP Levels").

#### Optional Fields

* **Description** → Brief explanation of the group.
* **Image**→ Visual representation (e.g., badge icon).
* **Custom Attributes** → Additional metadata (e.g., "color": "gold").

#### Steps

* Click "Create Tier Group".
* Enter a Title (required).
* (Optional) Add a Description, upload an Image, or define Attributes.
* Click "Save" to create the group.