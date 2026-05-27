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

> **(Rule-1 OR Rule-2..) AND (Rule-3 OR Rule-4...)**

with certain guardrails:

* Only allowed attributes, conditions and operators must be used.
* Leaf nodes must always have (attribute, condition, value) combination
* At max,  rules should be added.
* Root operator should be AND, even though it's always internally normalized to set it to AND.

<br />

## List of Available Conditions

<br />

| Operator                 | Key                   | Accepted Values                               |
| :----------------------- | :-------------------- | :-------------------------------------------- |
| Equals                   | equals                | String, number, datetime                      |
| Not Equals               | not_equals            | String, number, datetime                      |
| Greater Than or Equal to | greater_than_or_equal | String, number, datetime                      |
| Less Than or Equal to    | less_than_or_equal    | String, number, datetime                      |
|  Greater Than            | greater_than          | String, number, datetime                      |
| Less Than                | less_than             | String, number, datetime                      |
| Contains                 | contains              | String                                        |
| Not Contains             | not_contains          | String                                        |
| Ends With                | ends_with             | String                                        |
| In                       | in                    | List of String, number, datetime              |
| Not In                   | not_in                | List of String, number, datetime              |
| Between                  | between               | List of two values (String, number, datetime) |
| Before                   | before                | Datetime                                      |
| After                    | after                 | Datetime                                      |
| Within Last X Days       | within_last_x_days    | Integer                                       |
| Is                       | is                    | True, False                                   |
| Is Empty                 | is_empty              | True, False                                   |
| Is Not Empty             | is_not_empty          | True, False                                   |

## List of Available Attributes

| Attribute             | Key                       | Description                         | Allowed conditions                                                                              |
| :-------------------- | :------------------------ | :---------------------------------- | :---------------------------------------------------------------------------------------------- |
| Total Comments Posted | **total_comments_posted** | Number of comments posted by a user | Between, Greater Than, Less Than, Greater Than or Equal, Less Than or Equal, Equals, Not Equals |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
|                       |                           |                                     |                                                                                                 |
