---
title: Delivery Channel – Webhooks
deprecated: false
hidden: true
metadata:
  robots: index
---
Webhooks are a mechanism for **LiveLike** to notify your application when certain events occur. When an event you're subscribed to happens, we send a POST request to the webhook URL you provide. This allows you to trigger workflows or process data automatically, though the notification may not occur immediately.

This guide will help you understand how to configure, subscribe to, and consume webhooks securely from our platform.

# What Are Webhooks?

Webhooks allow our platform to send real-time data to your systems when specific events happen. You provide us with a URL, and we’ll send event payloads to that URL as they occur. Webhooks help automate workflows by delivering notifications without the need for constant polling.

# Key Concepts

* **Webhook URL:** The endpoint where we will send the event data.
* **Payload:** The actual event data sent in the body of the request.
* **Signature:** A cryptographic hash of the payload that ensures the integrity and authenticity of the data.
* **Webhook Event Types:** Specific events that you can subscribe to in order to receive notifications. Common events include:
* **Event Subscriptions:** You can create subscriptions to listen for specific events. This allows you to manage which events you want to receive and helps reduce unnecessary traffic.

# [Webhook Event Types](https://docs.livelike.com/docs/webhook-events-payload)

You can subscribe to specific events that match your business needs. Here are some common event types:

* **reward-table-rewards-awarded**: Triggered when a user is rewarded with a specific [reward item](https://docs.livelike.com/docs/webhooks) from [reward table](https://docs.livelike.com/docs/webhooks).
* **badge-awarded**: Triggered when a user is rewarded with a specific badge.

Each event will deliver a payload containing the relevant data for that event, such as profile IDs, reward item IDs, etc.

# Webhook Subscription

Currently, LiveLike Admins configure your webhook settings for you. However, in the future, you'll have the ability to configure these details directly through an API or CMS.

**Information Required to Subscribe:**

* **Webhook URL:** The endpoint where the event data should be sent.
* **Events to Subscribe To:** The specific events you'd like to receive notifications for (like reward-item-rewarded).

# Authenticating Webhooks

To ensure that webhook requests are coming from **LiveLike** and haven't been tampered with, we sign each payload. The signature is included in the headers, and you can use it to verify the authenticity of the data.

**Signature Calculation**  
Each webhook payload is signed using a shared secret (your client secret). The process is as follows:

1. The payload is serialized into a JSON string.
2. The signature is created using **HMAC-SHA1** with your **client secret** and the serialized payload.
3. The resulting signature is sent in the **X-Webhook-Signature** header.

# Verifying the Signature

```node nodejs
const crypto = require('crypto');

// Example signature verification
function verifySignature(payload, signature, secret) {
  const hash = crypto.createHmac('sha1', secret)
                    .update(JSON.stringify(payload))
                    .digest('base64');
  return hash === signature;
}

```
```python python
import hmac
import hashlib
import base64
import json

def generate_signature(payload, secret):
    serialized_payload = json.dumps(payload, separators=(',', ':'))
    signature = hmac.new(
        secret.encode(),
        serialized_payload.encode(),
        hashlib.sha1
    ).digest()
    return base64.b64encode(signature).decode('utf-8')

def verify_signature(payload, signature, secret):
    expected_signature = generate_signature(payload, secret)
    return hmac.compare_digest(expected_signature, signature)

```

# Consuming Webhooks

When a webhook is triggered, the payload is sent to your specified URL. The payload includes the event type and associated data:

```json json
{
  	"id": "76f574bd-c986-40a2-84fe-5e551fdfe375",
    "event": "reward-table-rewards-awarded",
    "data": {
        "reward_transaction_id": "reward-transaction-id",
        "reward_item_id": "reward-item-uuid",
        "reward_item_amount": 100,
        "reward_item_balance": 1000,
        "reward_action_id": "action-uuid",
        "reward_action_key": "play-game",
        "reward_table_id": "table-uuid",
        "client_id": "client-id",
        "profile_id": "profile-uuid",
        "profile_custom_id": "custom-id"
    },
    "created_at": "2024-09-02T12:34:56Z"
}

```

# Handling Webhook Requests

```node nodejs
const express = require('express');
const app = express();

app.use(express.json());

app.post('/webhooks', (req, res) => {
    const payload = req.body;
    const signature = req.headers['X-Webhook-Signature'];
    const secret = 'your-client-secret';

    if (verifySignature(payload, signature, secret)) {
        console.log('Verified webhook:', payload);
        res.sendStatus(200);
    } else {
        console.log('Invalid signature');
        res.sendStatus(400);
    }
});

app.listen(3000, () => console.log('Webhook server running on port 3000'));

```

# Best Practices

* Validate the signature to ensure the request is from us.
* Respond quickly with a 200 status code to acknowledge receipt.
* Keep in mind that the same webhook event may be delivered more than once, so having a plan to handle duplicates can be really helpful.
