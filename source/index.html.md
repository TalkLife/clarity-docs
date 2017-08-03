---
title: TalkLife Clarity Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - http

toc_footers:
  - <a href='https://talklifeclarity.com/app/keys'>View and Generate an API Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the TalkLife Clarity API Docs! Here you can find out how to interact with the Clarity API to send classification requests and recieve ML model outputs.

This API is currently in development and although we don't plan to make any breaking changes, we will give ample warning (to the email address on your developer account) if we change anything that may break your application.

# Authentication

> To authorize, use this code:

```http
GET /ping HTTP/1.1
Accept: application/json
Host: api.talklifeclarity.com
Authorization: <API KEY HERE>
```

> Make sure to replace `<API KEY HERE>` with your API key.

Clarity API uses API keys to allow access to the API. You can register a new Clarity API key in our [dashboard](https://talklifeclarity.com/app/keys).

Clarity API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <API KEY HERE>`

<aside class="notice">
You must replace <code>&lt;API KEY HERE&gt;</code> with a valid API key generated on your dashboard.
</aside>

# Classify

## Classify a single content

```http
POST /classify HTTP/1.1
Accept: application/json
Host: api.talklifeclarity.com
Authorization: <API KEY HERE>
Content-Length: 78

{
   "reference_id": 1,
   "content": "An example piece of content to demo on the docs"
}
```

```http
HTTP/1.1 201 OK
Content-Type: application/json

{  
   "reference_id": 1,
   "content": "An example piece of content to demo on the docs",
   "models":{  
      "agitation_or_irritation_suspected": false,
      "alcohol_and_substance_abuse_suspected": false,
      "anxiety_panic_fear_suspected": false,
      "behavorial_symptoms_suspected": false,
      "body_image_eating_disorders_suspected": false,
      "crying_suspected": false,
      "death_of_other_suspected": false,
      "depressed_mood_suspected": true,
      "distorted_thinking_suspected": false,
      "emotional_exhaustion_suspected": false,
      "emptiness_suspected": false,
      "failure_suspected": false,
      "family_issues_suspected": false,
      "final_tired_fatigued_low_energy_suspected": false,
      "helplessness_hopelessness_suspected": false,
      "inpatient_outpatient_medication_suspected": false,
      "loneliness_suspected": false,
      "mental_health_treatment_suspected": false,
      "nausea_suspected": false,
      "nausea_with_eating_disorder_suspected": false,
      "nssi_ideation_and_behavior_suspected": false,
      "nssi_urge_suspected": false,
      "numbness_emptiness_suspected": false,
      "numbness_suspected": false,
      "self_harm_relapse_suspected": false,
      "self_harm_remission_suspected": false,
      "song_lyrics_suspected": false,
      "suicidal_ideation_suspected": false,
      "suicidal_planning_suspected": false,
      "suicide_attempt_suspected": false,
      "tired_fatigued_low_energy_suspected": false
   }
}
```

This endpoint is used to classify a single content taking in input text and returning the standard Clarity models.

Each request to this endpoint (even with duplicate content) will be billed to your account as single classification.

### HTTP Request

`POST https://api.talklifeclarity.com/classify`

### Body Parameters

Parameter | Description
--------- | -----------
reference_id | This is a reference ID from your system (such as a Post ID)
content | This is the body content that you want to be classified

## Classify a batch of contents

```http
POST /classify/batch HTTP/1.1
Accept: application/json
Host: api.talklifeclarity.com
Authorization: <API KEY HERE>
Content-Length: 78

{
   "items": [
      {
         "reference_id": 1,
         "content": "An example piece of content to demo on the docs"
      },
      {
         "reference_id": 2,
         "content": "Another random piece of content for classification"
      },
      {
         "reference_id": 3,
         "content": "A third example post to be classified"
      }
   ]
}
```

```http
HTTP/1.1 201 OK
Content-Type: application/json

[
   {  
      "reference_id": 1,
      "content": "An example piece of content to demo on the docs",
      "models":{  
         "agitation_or_irritation_suspected": false,
         "alcohol_and_substance_abuse_suspected": false,
         "anxiety_panic_fear_suspected": false,
         ...
      }
   },
   {  
      "reference_id": 2,
      "content": "Another random piece of content for classification",
      "models":{  
         "agitation_or_irritation_suspected": false,
         "alcohol_and_substance_abuse_suspected": false,
         "anxiety_panic_fear_suspected": false,
         ...
      }
   },
   {  
      "reference_id": 3,
      "content": "A third example post to be classified",
      "models":{  
         "agitation_or_irritation_suspected": false,
         "alcohol_and_substance_abuse_suspected": false,
         "anxiety_panic_fear_suspected": false,
         ...
      }
   }
]
```

This endpoint is used to classify a batch of content's, like the single classification endpoint it will classify each content and return the standard Clarity models that were triggered. Sending a batch of content's is much faster than if you were to request each classification individually.

The cost of sending items in a batch request is the as sending them each individually, however its much faster.

### HTTP Request

`POST https://api.talklifeclarity.com/classify/batch`

### Body Parameters

Parameter | Description
--------- | -----------
items | This is the array of contents that need to be classified
items.reference_id | This is a reference ID from your system (such as a Post ID) for the item in the batch
items.content | This is the body content of the item in the batch that you want to be classified

<aside class="notice">The max batch size is 50 items and the request will fail if more items are provided</aside>