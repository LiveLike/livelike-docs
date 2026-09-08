---
title: Chat Room Sharding
deprecated: false
hidden: true
metadata:
  robots: index
---
## Overview

At high concurrency, a single chat room becomes hard to follow, messages scroll faster than anyone can read them.

Sharding splits one logical chat room into several parallel message streams ("shards"). Each user is assigned to one shard and sees the conversation happening there. The room itself doesn't change: one chat room ID, one configuration, one set of moderator controls. Sharding only changes which messages a given user actually receives.
