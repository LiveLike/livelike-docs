---
title: Localization
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Overview

Resources that support localization can store and return localized field values based on the language specified in the request header. Only specific fields within a resource are translatable, such as title, description, or question and these fields vary by resource. For example:

* The Poll resource has `question` field that can be localized.
* Its child resource, Poll Option, has `description` field that can be localized.

If a localized value for a requested language is not available or is null, clients would gracefully fall back to the default (base) value of that field.

Localization selection would follow a “best-match” strategy. For instance, if the client requests `en-GB` but only `en` is available, the system will return the `en` version.

## How do we determine the Languages to Consider for translation

When a user (or SDK) makes a request to our API, they can indicate their language preference using the standard `Accept-Language` header. This header can contain one or more language codes. For example:

`Accept-Language: fr-CA, en-US;q=0.9, es;q=0.8`

This tells us the user prefers(in given order preference):

1. Canadian French (`fr-CA`)
2. American English (`en-US`)
3. Spanish (`es`)

We can accept any tag from the industry-standard [IANA lang tag registry](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)

## How do we match Languages

We support full language tags, including script and region codes (e.g., `zh-Hant-TW`, `en-GB`), allowing for precise localization like UK vs US English or Simplified vs Traditional Chinese.  When a language code comes in uppercase or mixed case, we convert it to a standard format first before checking if we have a translation for it. This ensures that language codes like EN-us or en-US are treated the same.

Here’s the step-by-step logic we use to determine which translation to return:

1. **Exact Match First (Case insensitive)**

We check if the exact language requested (like `fr-CA`) exists in our translations. If yes, we use it directly.\
we do this exact matching for all languages provided in header regardless of their quality score(weight).

2. **Closest Match**

If no exact match is found, we try to find the closest alternative. For example:

* If the user asks for `en-AU` but we only have `en` or `en-UK`, We use `en` or `en-UK` accordingly.
* If the user asks for `zh-HK` (Hong Kong Chinese) and we only have `zh-Hant-HK`, we use that because it’s the closest match.

3. **Fallback to Default**

If no exact or closest match is found, we fall back to a default field value.

## API

### Retrieving Localized data

**Localized Program Resource**

`curl --request GET "https://cf-blast.livelikecdn.com/api/v1/programs/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/" -H "Accept-Language: fr"`

This retrieves the Program resource with translatable fields (e.g., `title`) localized in French (`fr`), if available.

**Localized Text Poll Resource**

`curl --request GET "https://cf-blast.livelikecdn.com/api/v1/text-polls/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/" -H "Accept-Language: en-GB"`

This retrieves the Text Poll Widget resource with allowed fields localized in British English (`en-GB`), if available.

### Adding or Updating Localized data

Translations can be added or updated via standard POST, PUT, or PATCH requests, depending on the use case.

To create or update a localized data, include a `localized_data` object in the request payload.

Example: Creating a Program with French and British English Translations

**Localized Program Resource**

```curl curl
curl --request POST \ 
 --url https://cf-blast.livelikecdn.com/api/v1/programs/ \
 --header 'Authorization: Bearer **************' \
 --header 'content-type: application/json' \
 --data '{
    "client_id": "*********************",
    "title": "An Awesome Program",
    "scheduled_at": "2025-06-02T04:14:23.148Z",
    "localized_data": {
      "fr": {
        "title": "Un programme génial"
      },
      "en-UK": {
        "title": "A Smashing Programme"
      }
    }
}'
```

<br />

#### PUT vs PATCH for Translations

* **PUT:** Replaces all existing translation data with the new payload. Use when you want to fully overwrite translations.
* **PATCH:** Merges new translations with existing ones. Ideal for updating or adding specific locales without affecting others.