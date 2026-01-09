---
title: Customer Data Platform
deprecated: false
hidden: false
metadata:
  robots: index
---
# Sweepstakes CDP Integration Guide

## Overview

This document outlines the integration of a Customer Data Platform (CDP) with the Sweepstakes application using a global JavaScript function hook. This approach enables real-time validation and enrichment of user entries by allowing the client to inject custom logic via a well-defined browser API before finalizing sweepstakes participation.

## Integration Flow

### 1. Define the Integration Hook

Clients (integrators) must define a global function on the window object before the sweepstakes app loads:

```js
window.LLSweepstakesCDPInvoke = async function (payload) {
	// Call your API or run custom validation logic
	const response = await yourApiCall(payload).catch(() => null)
	if (response && response.ok) {
		// Optionally, you can return a custom message as well
		return { flag: true, message: 'Entry successful! Good luck!' }
	}
	return { flag: false, message: 'You are not eligible for this sweepstakes.' }
}
```

* `payload` contains user and sweepstakes context.
* The function must return a Promise that resolves to an object with:
  * `flag` (boolean): allow or block entry
  * `message` (string): message to show to the user

### 2. App Calls the Hook

* When a user attempts to enter a sweepstakes, the app calls `window.LLSweepstakesCDPInvoke(payload)`.
* The app awaits the result and inspects the returned `flag` and `message`:
  * If `flag` is `true`, the app proceeds to add the user's entry and may display the message as confirmation.
  * If `flag` is `false`, the app does **not** add the entry and displays the provided message as feedback or error.
* If the function is not defined, or if it throws or returns no data, the app defaults to allowing the entry and proceeds as usual.

#### Example Response

```json
{
	"flag": true,
	"message": "Entry successful! Good luck!"
}
```

## Technical Details

* **Integration Hook**: The function `window.LLSweepstakesCDPInvoke` must be defined globally before the sweepstakes app is initialized.
* **Payload**: The app will pass a JSON object with user and sweepstakes context.
* **API Contract**: The function should return a Promise resolving to an object with `flag` and `message`.
* **Timeouts & Fallbacks**: If the function is not defined, throws, or does not resolve in a reasonable time, the app will proceed with entry to ensure a seamless user experience.
* **Extensibility**: This approach allows for future enhancements, such as enriching user profiles, applying business rules, or integrating with loyalty programs, all via the client’s own logic.

## Example Use Cases

* **Eligibility Checks**: Prevent duplicate entries, enforce age/location restrictions, or validate user status using your own backend or business logic.
* **Custom Messaging**: Display personalized messages, promotional codes, or next steps based on your API’s response.
* **Data Enrichment**: Augment entry data with additional attributes from the CDP for downstream analytics, all handled in your integration function.

## Highlights

* **Seamless Validation**: Integrate your business rules directly into the sweepstakes flow by simply defining a global function—no changes to the core app required.
* **Real-Time Feedback**: Provide users with instant, personalized feedback or instructions at the point of entry, based on your own API or logic.
* **Flexible & Future-Proof**: The integration is designed to be extensible, supporting a wide range of validation and enrichment scenarios as your needs evolve, all controlled by your implementation of the global hook.

## Summary

This CDP integration empowers clients to control sweepstakes entry logic and messaging dynamically, ensuring compliance, personalization, and a superior user experience—all with minimal changes to the core application. By simply defining the `window.LLSweepstakesCDPInvoke` function, you gain full control over entry validation and messaging, making the integration both powerful and easy to adopt.
