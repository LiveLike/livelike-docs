---
title: Comment Quality pipeline
deprecated: false
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
## Payload

<Table>
  <thead>
    <tr>
      <th style={{ width: "29.6%" }}>
        Field
      </th>

      <th style={{ width: "28.4%" }}>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
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
        `"comment_quality"`
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
        `true` returns at once with a `url` to poll. `false` waits up to about 25 seconds for the result.
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
        Any of the rule fields below.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.min_char_count`
      </td>

      <td>
        integer ≥ 0
      </td>

      <td>

      </td>

      <td>
        Minimum number of characters, not counting whitespace. `0` turns it off.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.disallowed_chars`
      </td>

      <td>
        string, max 64 chars
      </td>

      <td>

      </td>

      <td>
        Fails if the text contains any of these characters.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.emoji_ratio_threshold`
      </td>

      <td>
        number 0–1 or `null`
      </td>

      <td>

      </td>

      <td>
        Maximum share of the text that can be emoji (inclusive). `null` turns it off.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.exclude_gif`
      </td>

      <td>
        boolean
      </td>

      <td>

      </td>

      <td>
        Fails comments that contain a GIF.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.min_sentiment_score`
      </td>

      <td>
        number −1 to 1 or `null`
      </td>

      <td>

      </td>

      <td>
        Minimum sentiment (−1 negative, 0 neutral, 1 positive). `null` turns it off.
      </td>
    </tr>

    <tr>
      <td>
        `override_config.max_toxicity_score`
      </td>

      <td>
        number 0–1 or `null`
      </td>

      <td>

      </td>

      <td>
        Maximum toxicity. `null` turns it off.
      </td>
    </tr>
  </tbody>
</Table>

### Payload examples

```json With Direct Text
{
  "pipeline": "comment_quality",
  "text": "gg 🔥🔥🔥",
  "async": false,
  "override_config": {
    "min_char_count": 3,
    "emoji_ratio_threshold": 0.5,
    "max_toxicity_score": null
  }
}
```
```json With Comment ID
{
  "pipeline": "comment_quality",
  "comment_id": "8be4df61-93ca-11d2-aa0d-00e098032b8c",
  "async": false,
  "override_config": {
    "min_char_count": 3,
    "emoji_ratio_threshold": 0.5,
    "max_toxicity_score": null
  }
}
```

If your application has no saved quality rules, the defaults are used. A reply's `comment_id` always fails `min_char_count` with the value `"reply"`, because only top-level comments can be quality comments.

<br />

## Response
