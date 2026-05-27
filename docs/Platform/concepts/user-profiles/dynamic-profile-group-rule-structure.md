---
title: Dynamic Profile Group Rule Structure
excerpt: >-
  This page provides an overview of the rule creation flow for Dynamic Profile
  Groups via APIs.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Basic Rule Tree Sructure

The rule trees to be passed in the JSON payload for profile group creation API follow a basic structure as shown below:

```json
{
  "operator": "AND",
  "children": [
    {
      "operator": "OR",
      "children": [
        {
          "attribute": "attribute_1",
          "condtion": "condition_1",
          "value": "value_1"
        },
        {
          "attribute": "attribute_2",
          "condition": "condition_2",
          "value": "value_2"
        }
      ]
    },
    {
      "operator": "OR",
      "children": [
        {
          "attribute": "attribute_3",
          "condtion": "condition_3",
          "value": "value_3"
        },
        {
          "attribute": "attribute_4",
          "condition": "condition_4",
          "value": "value_4"
        }
      ]
    }
  ]
}
```

We create rule groups with **OR** operators between them and combine them with **AND**.

The structure is always maintained like:

> **(Rule-1 OR Rule-2) AND (Rule-3 OR Rule-4)**

<br />
