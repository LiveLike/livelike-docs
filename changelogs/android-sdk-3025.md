---
title: Android SDK 3.0.25
author: Viktor Manev
hidden: true
published_at: '2026-10-27T12:03:27.024Z'
type: added
---
Comment Report Threshold Feature

## Overview

Added optional `excludeCommentReportThreshold` to comment client requests, comment sessions, and comment feed counts.

## Usage

Pass a positive integer such as 1, 2, 5 ... to exclude comments at or above that report count. Reported parents with replies remain visible.

## Configuration

- **Default value:** `null` (omits the threshold filter)
- **Valid values:** Positive integers only
- **Invalid values:** Zero and negative values

## Deprecation Notice

`withoutReportedThread` in request-option classes has been deprecated and documented in `createCommentSession`. It remains functional for backward compatibility.

**Migration:** Use `excludeCommentReportThreshold = 1` for the previous enabled behavior.<br /><br /><br />more info & parameters: [https://docs.livelike.com/reference/list-comments](https://docs.livelike.com/reference/list-comments "https://docs.livelike.com/reference/list-comments")