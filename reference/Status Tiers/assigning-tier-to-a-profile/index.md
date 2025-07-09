---
title: Assigning tier to a profile
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
This API allows you to assign, upgrade, downgrade, or unassign a tier for a profile within a specific **Tier Group** — for example, a loyalty tier group like `Loyalty Tiers` with levels such as `Bronze`, `Silver`, and `Gold`.

#### How It Works

* **Initial Assignment**: Assigning a tier to a profile for the first time is considered an **upgrade** (e.g., assigning `Bronze` initially).
* **Upgrade**: Moving the profile from a lower tier to a higher one (e.g., `Bronze` → `Gold`).
* **Downgrade**: Moving the profile from a higher tier to a lower one (e.g., `Gold` → `Silver`).
* **Unassignment**: Removing the current tier assignment by passing `tier_id` as `null`.

All of these actions—initial assignment, upgrade, downgrade, and unassignment—can be performed using this single API.

***

#### Request

**Endpoint**: [Assign Tier](https://docs.livelike.com/reference/create-a-user-tier)\
**Body Parameters**:

| Field     | Type              | Description                                                |
| --------- | ----------------- | ---------------------------------------------------------- |
| `tier_id` | string\|null      | ID of the tier to assign. Use `null` to unassign the tier. |
| `reason`  | string (optional) | Optional reason for the change.                            |

***

#### Response Codes

| Status Code      | Description                                                                                                     |
| ---------------- | --------------------------------------------------------------------------------------------------------------- |
| `201 Created`    | Tier assigned for the **first time** to the profile.                                                            |
| `200 OK`         | Tier **updated**: either an upgrade or downgrade.                                                               |
| `204 No Content` | Tier **unassigned**, typically due to a downgrade from the lowest tier. Profile will now have no tier assigned. |

***

<br />

#### Behind the Scenes

When assigning a tier (e.g., level 3), the system automatically grants all lower tiers as well. For example:

* Assigning Level 3 → The profile receives Level 1, Level 2, and Level 3.

If the tier is removed (tier\_id: null), the system revokes all tiers, creating a series of downgrade entries in descending order:

1. Downgrade from Level 3 → Level 2
2. Downgrade from Level 2 → Level 1
3. Downgrade from Level 1 → no tier

These are reflected as multiple entries in the Tier Assignment API response.

<br />

#### Example Scenarios

* Assigning `Bronze` to a profile with no existing tier → `201 Created`
* Upgrading from `Bronze` to `Gold` → `200 OK`
* Downgrading from `Gold` to `Silver` → `200 OK`
* Removing a profile’s tier completely → pass `tier_id: null` → `204 No Content`