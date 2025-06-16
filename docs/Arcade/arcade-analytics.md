---
title: Arcade Analytics
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: Check out what events you can track for each of the MiniGames below
  pages:
    - type: basic
      slug: play-predictor-events
      title: Play Predictor Events
---
This document outlines the analytics event system implemented in the arcade application. It explains how to listen for emitted events, capture relevant data, and forward it to an analytics provider of your choice for tracking and analysis.  

## **Implementation**

Once integrated with any arcade game, you can listen for analytics events emitted by the application. These events are dispatched with the event name **`analytics-event`**.  

### **How to Listen for Analytics Events**

To capture analytics events in your application, use the following approach:  

```javascript
window.addEventListener('analytics-event', (event) => {
    const { eventName, eventData } = event.detail;
    console.log(`Event Captured: ${eventName}`, eventData);
    
    // Forward the event data to your analytics provider
    yourAnalyticsProvider.track(eventName, eventData);
});
```

Each event contains structured data, including metadata, user details, and event-specific properties.  

## **Event Data Structure**

Each emitted event contains the following key components:  

- **`event_name`** – Name of the triggered event.  
- **`event_properties`** – Custom properties specific to the event. 
  - **`default_user_properties`** – Details about the user.  (_Sent as default in each event._)
  - **`default_event_properties`** – Application level metadata.  (_Sent as default in each event._)

## **More about Default Properties**

### **User Properties**

The `user_properties` object contains user-specific details:  

- **`ll_username`** – The username.  
- **`ll_user_id`** – Unique user identifier.  
- **`is_new_user`** – Indicates if the user is new (`true/false/null`).  
- **`device_type`** – The user’s device type.  
- **`browser`** – The browser used.  
- **`platform`** – The user’s operating system or platform.  

### **Application Metadata**

The `defaultEventProperties` object contains general metadata about the application:  

- **`ll_org_name`** – Organization name.  
- **`ll_org_id`** – Unique organization identifier.  
- **`ll_app_name`** – Application name.  
- **`ll_app_id`** – Unique application identifier.  
- **`ll_instance_id`** – Unique instance identifier.