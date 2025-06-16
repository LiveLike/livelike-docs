---
title: Applications
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
An Application is the top-level resource in the REST API.  It must be created and managed through LiveLike's [Producer Suite](https://producer.livelikecdn.com).

# Fetching an Application

Once you have created an Application you can fetch details about the application through the REST API with:

### Request

```http
GET /api/v1/applications/UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO/ HTTP/1.1
```

### Response

```json
{
  "url": "https://cf-blast.livelikecdn.com/api/v1/applications/UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO/",
  "name": "ACME Sports!",
  "client_id": "UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO",
  "media_url": "https://cf-blast.livelikecdn.com/api/v1/media/?client_id=UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO",
  "pubnub_subscribe_key": "sub-c-1d9bd74e-fa13-4cf8-91ef-6e17a1479b01",
  "sendbird_app_id": "038D7DD3-81E9-420B-84D4-C2820941FAEC",
  "sendbird_api_endpoint": "https://api-us-2.sendbird.com/",
  "sessions_url": "https://cf-blast.livelikecdn.com/api/v1/applications/UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO/sessions/",
  "profile_url": "https://cf-blast.livelikecdn.com/api/v1/applications/UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO/profile/",
  "sticker_packs_url": "https://cf-blast.livelikecdn.com/api/v1/sticker-packs/?client_id=UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO",
  "image_url": "https://cf-blast-storage.livelikecdn.com/assets/37f7f9bf-4b0b-4ec3-955c-24f65eae9282.png",
  "programs_url": "https://cf-blast.livelikecdn.com/api/v1/programs/?client_id=UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO",
  "program_detail_url_template": "https://cf-blast.livelikecdn.com/api/v1/programs/{program_id}/",
  "mixpanel_token": "1517556f5e97ab3dfe3d8d8ee7811a3a",
  "organization_id": "a030a423-f7e0-46e2-81c0-8fbabdb0daf0",
  "organization_name": "ACME Sports, Inc.",
  "analytics_properties": {
    "Internal App ID": "UJQCf1jWIhKmQpOYdhe6H56Uc4Xp50b1zdVaOowO",
    "Internal App Name": "ACME Sports!",
    "Organization ID": "a030a423-f7e0-46e2-81c0-8fbabdb0daf0",
    "Organization Name": "ACME Sports, Inc."
  }
}

```
