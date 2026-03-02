---
title: Reciprocal Profile Blocking APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The current system supports one-way profile blocking using:
/POST /api/v1/profile-blocks/

* Authenticated user A blocks user B
* Creates a single DB row: (A → B)
* One-way relationship only

***

# Objective

Enhance the system to support:

* Reciprocal (two-way) blocking
* Client-level block policy configuration
* Flexible unblocking mechanisms
* Bulk block synchronization
* Policy-based enforcement (Active / Passive / Disabled)

***

# Schema

## Current Schema

```
class BlockApplicationProfile(UUIDModel):
    blocked_profile = models.ForeignKey(
        ApplicationProfile, related_name="blocked_profile", on_delete=models.CASCADE
    )
    blocked_by_profile = models.ForeignKey(
        ApplicationProfile, related_name="blocked_by_profile", on_delete=models.CASCADE
    )
    created_at = models.DateTimeField(default=timezone.now)

```

## Add Block Policy at Application Level

Add block_policy field to Application model.
This setting:

* Controls block enforcement behavior
* Has highest priority
* Overrides default configuration
* Applies globally per client

```python BlockPolicy
class BlockPolicy(models.TextChoices):
    DISABLED = "disabled", "Disabled"
    ACTIVE_ONLY = "active_only", "Active Only"
    ACTIVE_AND_PASSIVE = "active_and_passive", "Active and Passive"

```

### Field Definition:

```python
block_policy = models.CharField(
    max_length=20,
    choices=BlockPolicy.choices,
    default=BlockPolicy.ACTIVE_AND_PASSIVE,
)

```

## Policy Behavior

### **DISABLED**

* No blocking applied anywhere
* All interactions allowed
* Blocks ignored entirely

### **ACTIVE_ONLY**

* Only write interactions blocked:
* Comment creation
* Chat message creation
* Mentions
* Reactions
* Read operations not blocked

### **ACTIVE_AND_PASSIVE (Default)**

Block applies to:

* Write interactions
* Read interactions (content visibility)

***

# Blocking Behavior

If blocking is enabled:

* Blocking is always reciprocal
* Any block relationship between two users is treated as mutual restriction
* Applies based on block policy

***

# APIs

**Existing endpoint**

POST /api/v1/profile-blocks/

**Behavior**:

* Creates block entry
* Reciprocal enforcement handled at policy layer

## Remove Reciprocal Block

Existing endpoint

DELETE /api/v1/profile-blocks/{'{db_object_id}'}

## Remove Reciprocal Block

* Same behavior as existing unblock endpoint
* Alternative path for client convenience

DELETE /api/v1/profiles/{'{blocked_by_profile_uuid}'}/profile-blocks/{'{blocked_profile_id}'}/

## Remove Reciprocal Block (Custom ID)

Same behavior as existing unblock endpoint

POST /api/v1/profile-blocks/bulk-sync/

## Bulk Sync Block List

POST /api/v1/profile-blocks/bulk-sync/

## Bulk Sync Block List

POST /api/v1/profile-blocks/bulk-sync/

**Payload**

```
{
  "blocks": [
    {
      "blocked_by_profile_id": "<uuid>",
      "blocked_profile_id": "<uuid>"
    }
  ],
  "override": true
}

```

### Rules

* Maximum 1000 items per request (configurable)
* Both profiles must belong to same application
* Cannot block self
* override=true:
  * Deletes existing block entries
  * Replaces with new list
* override=false:
  * Appends to existing list

### Rationale

* Limit prevents:
* Long DB locks
* Timeouts
* Retry storms
* Memory spikes

## Configure Block Policy

Using existing Application APIs:

POST /api/v1/applications/
PATCH /api/v1/applications/

Payload:

```json
{
  "block_policy": "active_only"
}

```

Default:

```text nginx
active_and_passive
```

***

# Technical Enforcement

### Blocking Active Actions

Used in comment creation, mentions, reactions, etc.

```python
def is_action_blocked(viewer, other):
    block_policy = profile.application.block_policy

    if block_policy == BlockPolicy.DISABLED:
        return False

    return is_blocked_or_has_blocked(viewer, other)

```

#### Behavior

| Policy             | Result                       |
| :----------------- | :--------------------------- |
| DISABLED           | Always False                 |
| ACTIVE_ONLY        | Block if relationship exists |
| ACTIVE_AND_PASSIVE | Block if relationship exists |

### Filtering Query Results (Passive)

Used in read operations (comments, chat messages, boards, etc.)

```python
def exclude_blocked(qs, viewer, author_field):
```

**Logic**
If:

* Policy = DISABLED → No filtering
* Policy = ACTIVE_ONLY → No filtering
* Policy = ACTIVE_AND_PASSIVE → Apply filtering

Filtering excludes rows where:

* Viewer blocked author
  OR
* Author blocked viewer

## Enforcement

| Policy             | Write Blocked | Read Blocked |
| ------------------ | ------------- | ------------ |
| DISABLED           | ❌             | ❌            |
| ACTIVE_ONLY        | ✅             | ❌            |
| ACTIVE_AND_PASSIVE | ✅             | ✅            |

## Design Considerations

* Backward compatible
* No schema change required for BlockApplicationProfile
* Application-level override gives client flexibility
* Supports enterprise clients with external moderation systems
* Supports bulk migration from legacy systems

## Implementation Notes

* Reciprocal enforcement handled logically, not physically
* DB structure remains one-directional
* Query filtering applied dynamically
* Bulk sync should use transaction + batching
* Validation required at serializer level
