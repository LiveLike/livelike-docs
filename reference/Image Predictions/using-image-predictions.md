---
title: Using Predictions
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
The prediction experience is consists of two widgets: a prediction and a follow-up. The first widget sets up the question, and the second widget reveals the answer. When someone sees a prediction widget, they are given an opportunity to read the question and pick their answer. Then when they see the follow-up, they will learn whether or not they were right.

Rewards associated with a prediction widget can be claimed after the follow-up is published.  When a user makes their initial selection they are issued a `claim_token`.  This token should be stored by the application so that it can be submitted in order to claim any follow-up rewards.  The follow-up widget resource has a `claim_url` field.  In order to claim the rewards the app should submit the user's `claim_token` to the `claim_url`.  If any rewards are unlocked then they will be returned in the response in the same way as rewards for normal interactions.
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"claim_token\": \"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbmNyeXB0ZWQiOiJnQUFBQUFCaFM0a3VwbTJUVDBfNUFPaGFlUEpQR0VxeVhWTXA2V3hCOTNuQWEwbUVkSjByc29oaXZFNVVUaVdCN3ZmY05YVFladmYzWi1TdjRBb2k3Y3R1alBIcUFhT2FMWFNZQXZQckM3WGs4LVNoaURGWmJ3bl9ObF85N3Q1dzVUZGNZMktReXpJVTJqNDBvRXdaSGFLSW9vRDZOUU1xVTRQYkVkdzkwUXNqWlpkQ1YtaHN4ZXNsSkQ4SGFLTUpqWXNPQ25YQU9iLWkiLCJpc3MiOiJibGFzdCIsImlhdCI6MTYzMjMzOTg1N30.3ackVeJZFhPj9nLm8npJkeolTNfQJU1e7W8z9Rah8CI\",\n}",
      "language": "json"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "# Example prediction follow-up resource.  \n{\n  # Other widget fields omitted\n\t\"claim_url\": \"https://cf-blast.livelikecdn.com/api/v1/widget-interaction-claims/image-prediction/d645028b-6244-4e0b-acc5-f120a4171d83/claims/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbmNyeXB0ZWQiOiJnQUFBQUFCaFM0a3VwbTJUVDBfNUFPaGFlUEpQR0VxeVhWTXA2V3hCOTNuQWEwbUVkSjByc29oaXZFNVVUaVdCN3ZmY05YVFladmYzWi1TdjRBb2k3Y3R1alBIcUFhT2FMWFNZQXZQckM3WGs4LVNoaURGWmJ3bl9ObF85N3Q1dzVUZGNZMktReXpJVTJqNDBvRXdaSGFLSW9vRDZOUU1xVTRQYkVkdzkwUXNqWlpkQ1YtaHN4ZXNsSkQ4SGFLTUpqWXNPQ25YQU9iLWkiLCJpc3MiOiJibGFzdCIsImlhdCI6MTYzMjMzOTg1N30.3ackVeJZFhPj9nLm8npJkeolTNfQJU1e7W8z9Rah8CI/\",\n}",
      "language": "json"
    }
  ]
}
[/block]
Claim the prediction rewards
[block:code]
{
  "codes": [
    {
      "code": "POST /<claim_url>\nAuthorization: Bearer <profile_access_token>\nContent-Type: application/json\n\n{\n  \"claim_token\": \"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbmNyeXB0ZWQiOiJnQUFBQUFCaFM0a3VwbTJUVDBfNUFPaGFlUEpQR0VxeVhWTXA2V3hCOTNuQWEwbUVkSjByc29oaXZFNVVUaVdCN3ZmY05YVFladmYzWi1TdjRBb2k3Y3R1alBIcUFhT2FMWFNZQXZQckM3WGs4LVNoaURGWmJ3bl9ObF85N3Q1dzVUZGNZMktReXpJVTJqNDBvRXdaSGFLSW9vRDZOUU1xVTRQYkVkdzkwUXNqWlpkQ1YtaHN4ZXNsSkQ4SGFLTUpqWXNPQ25YQU9iLWkiLCJpc3MiOiJibGFzdCIsImlhdCI6MTYzMjMzOTg1N30.3ackVeJZFhPj9nLm8npJkeolTNfQJU1e7W8z9Rah8CI\",\n}",
      "language": "http"
    }
  ]
}
[/block]