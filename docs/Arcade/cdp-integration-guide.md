---
title: CDP Integration Guide
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

This document outlines a generic approach for integrating a Customer Data Platform (CDP) with any web application using a global JavaScript function hook. This enables real-time validation, enrichment, and messaging for any event (e.g., sweepstakes entry, purchase, registration) by allowing the client to inject custom logic via a well-defined browser API before finalizing the action.

## Integration Flow

### Payload Structure

The payload sent to `window.LLCDPInvoke` in the app follows this interface:

```typescript
interface LlCdpPayload {
	type?: string // Event type, e.g., 'sweepstakes_entry'
	gameId?: string // Sweepstakes/game identifier
	instanceId?: string // Instance identifier
	profileId?: string // User profile identifier
	data?: Record<string, string> // Arbitrary form or event data
}
```

Example payload:

```json
{
	"type": "sweepstakes_entry",
	"gameId": "abc123",
	"instanceId": "xyz789",
	"profileId": "user456",
	"data": {
		"email": "user@email.com",
		"name": "Jane Doe"
	}
}
```

### 1. Define the Generic Integration Hook

Clients (integrators) must define a global function on the window object before the app loads:

```js
window.LLCDPInvoke = async function (payload) {
	// payload.type indicates the event type (e.g., 'sweepstakes_entry', 'purchase', 'registration')
	// Call your API or run custom validation logic
	const response = await yourApiCall(payload).catch(() => null)
	if (response && response.ok) {
		// Optionally, you can return a custom message as well
		return { flag: true, message: 'Action allowed!' }
	}
	return { flag: false, message: 'Action not allowed.' }
}
```

* `payload` contains event type, user, and context (e.g., `{ type: 'sweepstakes_entry', ... }`).
* The function must return a Promise that resolves to an object with:
  * `flag` (boolean): allow or block the action
  * `message` (string): message to show to the user

### 2. App Calls the Hook

* When an event occurs (e.g., sweepstakes entry), the app calls `window.LLCDPInvoke(payload)`.
* The app awaits the result and inspects the returned `flag` and `message`:
  * If `flag` is `true`, the app proceeds and may display the message as confirmation.
  * If `flag` is `false`, the app does **not** proceed and displays the provided message as feedback or error.
* If the function is not defined, or if it throws or returns no data, the app defaults to allowing the action and proceeds as usual.

#### Example Response

```json
{
	"flag": true,
	"message": "Action allowed!"
}
```

## Technical Details

* **Integration Hook**: The function `window.LLCDPInvoke` must be defined globally before the app is initialized.
* **Payload**: The app will pass a JSON object with at least a `type` field and relevant context.
* **API Contract**: The function should return a Promise resolving to an object with `flag` and `message`.
* **Timeouts & Fallbacks**: If the function is not defined, throws, or does not resolve in a reasonable time, the app will proceed with the action to ensure a seamless user experience.
* **Extensibility**: This approach allows for future enhancements, such as enriching user profiles, applying business rules, or integrating with loyalty programs, all via the client’s own logic.

## Example Use Cases

* **Eligibility Checks**: Prevent duplicate actions, enforce restrictions, or validate user status using your own backend or business logic.
* **Custom Messaging**: Display personalized messages, promotional codes, or next steps based on your API’s response.
* **Data Enrichment**: Augment event data with additional attributes from the CDP for downstream analytics, all handled in your integration function.

## Highlights

* **Seamless Validation**: Integrate your business rules directly into any app flow by simply defining a global function—no changes to the core app required.
* **Real-Time Feedback**: Provide users with instant, personalized feedback or instructions at the point of action, based on your own API or logic.
* **Flexible & Future-Proof**: The integration is designed to be extensible, supporting a wide range of validation and enrichment scenarios as your needs evolve, all controlled by your implementation of the global hook.

## Summary

This generic CDP integration empowers clients to control business logic and messaging dynamically for any event or action, ensuring compliance, personalization, and a superior user experience—all with minimal changes to the core application. By simply defining the `window.LLCDPInvoke` function, you gain full control over validation and messaging, making the integration both powerful and easy to adopt across your entire web ecosystem.
