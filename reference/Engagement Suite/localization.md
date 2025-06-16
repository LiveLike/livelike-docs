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
Any resource that supports localization will have a `translations` property containing a mapping of localizable field names in the base resource to objects that map ISO 639 language codes to localized values. In this simplified poll example, the parent poll resource has a `question` field that can be localized to English and Spanish. The child poll option resources have a `description` field that can be localized similarly. Fields that can’t be localized don’t have corresponding keys in their sibling translations property. If the resource can’t be localized, it won’t have the translations property. If the field can be localized, but the value for the desired locale is missing or null, clients should fall back to using the corresponding property on the base resource.

```json
{
  "question":"Who will win?",
  "translations":{
    "question":{
      "en":"Who will win?",
      "es":"¿Quién ganará?"
    }
  },
  "options":[
    {
      "description":"Us",
      "translations":{
        "description":{
          "en":"Us",
          "es":"Nosotros"
        }
      }
    },
    {
      "description":"Them",
      "translations":{
        "description":{
          "en":"Them",
          "es":"Ellos"
        }
      }
    }
  ]
}
```

Clients should use a “best-match” approach when selecting a localized version. For example, if the client’s desired locale is `en-GB`, but only `en` is available, then the client should select the en locale.
