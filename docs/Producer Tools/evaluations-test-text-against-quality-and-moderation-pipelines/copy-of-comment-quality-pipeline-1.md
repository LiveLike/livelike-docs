---
title: Comment Moderation Pipeline
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: noindex
---
## Payload

<Table>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th style={{ width: "16.5%" }}>
        Type
      </th>

      <th style={{ width: "23.5%" }}>
        Required
      </th>

      <th style={{ width: "36.3%" }}>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `pipeline`
      </td>

      <td>
        string
      </td>

      <td>
        Yes
      </td>

      <td>
        `"comment_moderation"`
      </td>
    </tr>

    <tr>
      <td>
        `text`
      </td>

      <td>
        string, max 5000 chars
      </td>

      <td>
        One of `text` / `comment_id`
      </td>

      <td>
        Text to evaluate.
      </td>
    </tr>

    <tr>
      <td>
        `comment_id`
      </td>

      <td>
        UUID
      </td>

      <td>
        One of `text` / `comment_id`
      </td>

      <td>
        A comment in this application. Its text is evaluated.
      </td>
    </tr>

    <tr>
      <td>
        `async`
      </td>

      <td>
        boolean
      </td>

      <td>
        No (default `true`)
      </td>

      <td>
        `true` returns a `url` to poll. `false` waits up to about 25 seconds for the result.
      </td>
    </tr>

    <tr>
      <td>
        `override_config`
      </td>

      <td>
        object
      </td>

      <td>
        No
      </td>

      <td>
        `{category: threshold}`, where each threshold is a number from 0 to 1. A category is flagged when its score is **above** its threshold.
      </td>
    </tr>
  </tbody>
</Table>

### Payload Examples

```json With Direct Text
{
  "pipeline": "comment_moderation",
  "text": "<text to test>",
  "async": false,
  "override_config": {
    "insult": 0.5,
    "threat": 0.3
  }
}
```
```json With Comment ID
{
  "pipeline": "comment_moderation",
  "comment_id": "3f6b2c1e-8a4d-4f7e-9b2a-1c5d7e9f0a12",
  "async": false,
  "override_config": {
    "insult": 0.5,
    "threat": 0.3
  }
}
```

You can only use categories your configured moderation model emits, any other category returns `400`. Every evaluation's `effective_config` lists all the categories with their current thresholds. The model always comes from your saved configuration and can't be overridden.