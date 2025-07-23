---
title: Status Tiers
excerpt: Users can unlock benefits as they progress through status tiers
deprecated: false
hidden: false
metadata:
  robots: index
---
Use Status Tiers to define reward systems where users progressively unlock the benefits associated with those tiers. As users reach more advanced tiers, their benefits from them accumulate.

<Image align="center" width="40% " src="https://files.readme.io/8a5bb68d8eaf149eb16aee46ab54e8ea89ceb992861b22e772d5a1ff530131df-Status_Tiers_cropped.png" />

## Key Components

A *tier* represents a level of progress within a *tier group*.

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

***

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
* **Image**→ Visual representation.
* **Custom Attributes** → Additional metadata.

#### Steps

* Click "Create Tier Group".
* Enter a Title (required).
* (Optional) Add a Description, upload an Image, or define Attributes.
* Click "Save" to create the group.

***

<br />

### Adding Tiers to a Group

#### Required Fields

* **Title (Mandatory)** → Name of the Tier (e.g., "Gold")

#### Optional Fields

* **Description** → Brief explanation of the Tier.
* **Image**→ Visual representation.
* **Custom Attributes** → Additional metadata.

#### Configuration Options

* **Tier with Reward Threshold (Auto-Assignment)**
  * Enable **"Set Reward Threshold"**
  * Select a **Reward Item** (e.g., "Total Points")
  * Enter a **Threshold Value** (e.g., 1000)
  * Order is auto-set based on threshold (higher = higher tier)

* **Tier without Threshold (Manual Assignment)**
  * Leave **"Set Reward Threshold"** disabled
  * Order can be manually adjusted later

#### Steps

* Open the desired by clicking on View Detail of **Tier Group**
* Click **"Add Tier"**
* Enter a **Title** (required)
* Choose between:
  * **Auto-assignment**: Set reward threshold
  * **Manual-assignment**: Leave threshold empty
* Click **"Save"** to create the tier

#### Key UI Notes

**Tier Order Rules:**

* Threshold-based tiers are locked in auto-order.
* Manual tiers can be dragged/dropped to reorder.

***

<br />

### Adding Benefits Within a Tier

#### Required Fields

* **Title (Mandatory)** → Name of the Benefit (e.g., "Free Shipping", "Exclusive Discount")

#### Optional Fields

* **Description** → Additional details about the benefit
* **Image** → Visual representation (e.g., icon, badge)
* **Custom Attributes** → Metadata (e.g., `"expiry": "30d"`)

#### Rewardable Benefit (Optional)

* Enable **"Rewardable"** toggle to link a reward item
* **Reward Item** → Select from existing rewards (e.g., "Loyalty Points")
* **Reward Value** → Amount granted when the user reaches the tier (e.g., `100` points)

> When a user qualifies for the tier, they automatically receive the reward if the benefit is rewardable.

#### Steps

* Open the desired **Tier** inside a **Tier Group**
* Click **"Add Benefit"**
* Enter a **Title** (required)
* *(Optional)* Fill in **Description**, **Image**, or **Attributes**
* *(Optional)* Toggle **"Rewardable"** and link a **Reward Item** + **Value**
* Click **"Save"** to add the benefit

#### Example: Rewardable Benefit Setup

* **Tier**: `"Gold"`
* **Benefit Title**: `"Welcome Bonus"`
* **Rewardable**: ✅ Enabled
* **Reward Item**: `"Loyalty Points"`
* **Value**: `500`

**Result**: When a user hits the Gold tier’s threshold, they automatically get 500 loyalty points.

#### Key Rules

* Non-rewardable benefits are purely descriptive (e.g., `"24/7 Support"`)
* Rewardable benefits trigger instantly upon tier qualification
* Reward items must be pre-configured in the **Rewards System**

<br />

***

<br />

### Archiving Tier Groups, Tiers, and Benefits

#### Overview

* **Archiving** allows you to deactivate **Tier Groups, Tiers, or Benefits** without permanently deleting them
* Archived items appear in a dedicated **"Archived" tab** within their respective sections
* Archived items are **excluded** from active workflows (e.g., tier assignment, reward logic)
* Items can be **reactivated** or **permanently deleted** from the archive

#### Archiving a Tier Group

* **Effect**:
  * Archives the **entire group**, including all associated **tiers and benefits**
  * Users **cannot progress** in an archived group
  * Existing tier assignments remain but **stop updating**

* **Steps**:
  1. Go to **Status Tier > Tier Groups**
  2. Click the **"⋮" (More Options)** on the desired group
  3. Select **"Archive"**
  4. Confirm the action

#### Archiving a Tier

* **Effect**:
  * Only the selected **tier** is archived (group remains active)
  * Users **cannot qualify** for the tier if auto-assigned

* **Steps**:
  1. Open the **Tier Group** containing the tier
  2. Click the **"⋮"** next to the tier
  3. Select **"Archive"**

#### Archiving a Benefit

* **Effect**:
  * Benefit is removed from the tier but **preserved** in the archive
  * Existing users **retain previously granted rewards**
  * New tier qualifiers **do not receive** the benefit

* **Steps**:
  1. Open the **Tier** containing the benefit
  2. Click the **"⋮"** next to the benefit
  3. Select **"Archive"**

### Managing Archived Items

#### Accessing Archived Items

* Each section (**Tier Groups**, **Tiers**, **Benefits**) includes an **"Archived"** tab
* Switch to this tab to view, activate, or delete archived items

#### Actions Available

| Action       | Effect                                                  |
| ------------ | ------------------------------------------------------- |
| **Activate** | Restores the item (e.g., tier becomes assignable again) |
| **Delete**   | Permanently removes the item (**irreversible**)         |

#### Steps to Restore or Delete

1. Navigate to the **"Archived"** tab in the relevant section
2. Click **"⋮"** next to the item
3. Choose:
   * **"Activate"** → Returns the item to the active list
   * **"Delete Forever"** → Removes the item permanently

### Key Rules & Best Practices

⚠ **Tier Groups**:

* Reactivating a group **also restores** all its nested **tiers and benefits**
* Deleting a group **permanently removes** all associated content

♻ **Tiers/Benefits**:

* Reactivated tiers **resume original order and thresholds**

### Example Workflow

1. Archive the **"Bronze" tier** (threshold: 500 XP)
   * ➜ Users stop qualifying for Bronze
2. Later, **Activate** the Bronze tier from the Archived tab
   * ➜ Tier becomes active again and users can earn it

***

### Tier Ordering System

#### 1. Core Ordering Rules

##### Automatic-Order Tiers (With Thresholds)

* Ordered strictly by **reward threshold value** (low to high)
* Higher threshold = higher tier position
* Positions are **locked** and cannot be manually changed

##### Manual-Order Tiers (No Thresholds)

* New tiers are added to the **end** of non reward tiers.
* Can be **freely reordered** among other manual tiers
* Must always remain **below** automatic-order tiers

#### 2. Archival Behavior

##### When Archiving a Tier

* Tier is **removed** from the active sequence
* Other tiers maintain their **relative positions**
* No gaps are created in the ordering

##### When Reactivating a Tier

* Tier returns to its **original position**
  * For automatic tiers: May **reorder** other threshold tiers
  * For manual tiers: Returns to **saved position**, newer tiers shift down

#### 4. Special Cases

* Removing a tier’s threshold moves it to the **manual section**
* If all threshold tiers are archived, **manual ordering takes over**
* Updating a threshold triggers **automatic reordering** of all affected tiers

This system ensures:

* Logical, **threshold-based tier progression**
* Flexibility for **manually prioritized tiers**

***

### Benefit Ordering System

#### 1. Benefit Position Assignment

##### New Benefits

* Automatically assigned the **next available order number** when created
* Appears at the **bottom** of the benefit list by default

**Example:**

* Existing benefits: `[1]`, `[2]`, `[3]`
* New benefit added → Assigned order **`[4]`**

#### 2. Reordering Benefits

##### Manual Adjustment

* Benefits can be **freely reordered** using drag-and-drop or manual input
* Order numbers update **dynamically** during rearrangement
* No restrictions on positioning (unlike tier ordering)

##### User-Facing Impact

* Benefits are **shown to users in the defined order**
* Common use cases:
  * Highlight **most important** benefits first
  * Group **related** benefits
  * Promote **premium offerings** at the top

#### 3. Archival Behavior

##### When Archiving a Benefit

* Benefit is **removed** from the active list
* Remaining benefits **retain** their positions
* No gaps created in numbering

##### When Reactivating a Benefit

* Benefit is re-added to the to its original position.

#### 4. UI Implementation

* **Drag handles** are present on all benefits
* **Live preview** while reordering
* No lock icons — **all benefits are fully adjustable**

#### Example Workflow

1. **Initial List**:
   * `[1]` Free Shipping
   * `[2]` 24/7 Support
   * `[3]` Birthday Discount

2. **Add New Benefit**:
   * `[4]` Early Access → Auto-assigned to bottom

This system provides:

* **Full control** over benefit presentation
* **Flexible reordering** with no constraints