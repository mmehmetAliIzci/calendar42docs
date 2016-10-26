Scenario:

Lets say, there are 3 people who each own a car. All of them want to arrive at work at the same location at the same time. However, their homes are far away from each other. Our system will find the best match between all their travel-intents and create rideshares. Ideally all of them will have 2 rideshare options each. After the rideshares are created, users who are declared by driver_id and passenger_id should accept the rideshare. (You can see the rideshare state flow in the rideshare/states).

##### Set up and update the travel intents to get a successful rideshare.

There are 3 drivers who want to arrive to work at the same time.
Depending on their geological points they will be matched to share a ride and a rideshare will be generated.

POST: `https://dev04.c42.io/api/travel-intent/v1/travel-intent/`

```
{
    "user_id":"your-generated-version-4-UUID",
    "user_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "departure_geo_point": {
    "latitude": "52.011021",
    "longitude":"4.336688"
    },
    "arrival_geo_point": {
    "latitude": "52.165051",
    "longitude":"4.500659"
    },
    "extra": {"This intent is from":"driver"},    
    "timezone": "Europe/Amsterdam",
    "as_driver":true,
    "as_passenger":true,
    "arrival_time": {
        "max": "2016-10-24T20:31:19.073Z",
        "min": "2016-10-24T19:31:19.072Z"
    }
}
```
```
{
    "user_id":"your-generated-version-4-UUID",
    "user_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "departure_geo_point": {
    "latitude": "52.016475",
    "longitude":"4.363224"
    },
    "arrival_geo_point": {
    "latitude": "52.165051",
    "longitude":"4.500659"
    },
    "extra": {"This intent is from":"driver2"},
    "timezone": "Europe/Amsterdam",
    "as_driver":true,
    "as_passenger":true,
    "arrival_time": {
        "max": "2016-10-24T20:31:19.073Z",
        "min": "2016-10-24T19:31:19.072Z"
    }
}
```
```
{
    "user_id":"your-generated-version-4-UUID",
    "user_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "departure_geo_point": {
    "latitude": "52.051067",
    "longitude":"4.406224"
    },
    "arrival_geo_point": {
    "latitude": "52.165051",
    "longitude":"4.500659"
    },
    "extra": {"This intent is from":"driver3"},
    "timezone": "Europe/Amsterdam",
    "as_driver":true,
    "as_passenger":true,
    "arrival_time": {
        "max": "2016-10-24T20:31:19.073Z",
        "min": "2016-10-24T19:31:19.072Z"
    }
}
```

* Get generated rideshares for all drivers


GET: `https://dev04.c42.io/api/rideshare/v1/rideshare/?driver_id={{driver_id}}`

GET: `https://dev04.c42.io/api/rideshare/v1/rideshare/?driver_id={{driver_id2}}`

GET: `https://dev04.c42.io/api/rideshare/v1/rideshare/?driver_id={{driver_id3}}`

* Accept the rideshares

Driver accepts:
```
{
    "user_id": "your-generated-version-4-UUID",
    "action": "accept"
}
```
Passenger accepts:

```
{
    "user_id": "your-generated-version-4-UUID",
    "action": "accept"
}
```


---
Up to this point we were be able to
- Create `travel-intent`'s
- Get `rideshare` suggestions
- Accept the rideshares

Now lets say, we already know this scenario will keep happening all the days of the week for all the users. Instead of creating all the travel intents one by one, we can create `travel_intent_pattern`s and let our system generate all `travel-intent`s for us.

##### Create a travel intent pattern for a user.

POST: `https://dev04.c42.io/api/travel-intent-pattern/v1/travel-intent-pattern/`

BODY:

```
{
    "user_id":"your-generated-version-4-UUID",
    "user_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "departure_geo_point": {
        "latitude": 52.085165,
        "longitude": 5.116112
    },
    "arrival_geo_point": {
        "latitude": 52.334198,
        "longitude": 4.859670
    },
    "timezone": "Europe/Amsterdam",
    "extra": {"This works":"Well in the pattern API μService"},
    "as_driver":true,
    "as_passenger":true,
    "effective_date":"2016-07-29T10:11:18",
    "rrule": "FREQ=WEEKLY;BYDAY=MO,TU",
    "propagation_period":604800,
    "propagated_until": null,
    "arrival_time": {
        "max": "11:00:00",
        "min": "09:00:00"
    },
    "departure_time": null
}
```

RESPONSE:

```
{
  "meta_data": {},
  "data": [
    {
      "id": "73678a72-8764-4259-aff0-ffbefb6b2709",
      "departure_geo_point": {
        "latitude": 52.085165,
        "longitude": 5.116112
      },
      "arrival_geo_point": {
        "latitude": 52.334198,
        "longitude": 4.85967
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "ae228334-9d73-4971-8091-102c8ad85ed8",
      "community_id": "66f7b084-276d-444f-a376-b026a54e5b81",
      "created": "2016-10-24T12:19:53.902747Z",
      "modified": "2016-10-24T12:19:53.902770Z",
      "as_driver": true,
      "as_passenger": true,
      "timezone": "Europe/Amsterdam",
      "extra": {
        "This works": "if you want to send extra data along with post"
      },
      "propagation_period": 604800,
      "propagated_until": null,
      "effective_date": "2016-07-29T10:11:18Z",
      "rrule": "FREQ=WEEKLY;BYDAY=MO,TU",
      "arrival_time": {
        "max": "11:00:00",
        "min": "09:00:00"
      }
    }
  ]
}
```

##### Get your generated travel intents by querying travel-intent endpoint

GET: `https://dev04.c42.io/api/travel-intent/v1/travel-intent/?pattern_id=73678a72-8764-4259-aff0-ffbefb6b2709`

RESPONSE:

```
{
  "meta_data": {
    "count": 2, /*you have two travel intents because rrule is MO,TU*/
    "limit": 10,
    "offset": 0
  },
  "data": [
    {
      "id": "92e9d205-90a5-445f-9f13-c08eb20779a4",
      "departure_geo_point": {
        "latitude": 52.085165,
        "longitude": 5.116112
      },
      "arrival_geo_point": {
        "latitude": 52.334198,
        "longitude": 4.85967
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "ae228334-9d73-4971-8091-102c8ad85ed8",
      "community_id": "66f7b084-276d-444f-a376-b026a54e5b81",
      "created": "2016-10-24T12:19:54.037493Z",
      "modified": "2016-10-24T12:19:54.037517Z",
      "as_driver": true,
      "as_passenger": true,
      "extra": {
        "This works": "if you want to send extra data along with post"
      },
      "travel_time": 2945.03455714128,
      "travel_distance": 32722.6061904587,
      "pattern_id": "73678a72-8764-4259-aff0-ffbefb6b2709",
      "departure_time": {
        "max": "2016-10-25T09:00:00.000000Z",
        "min": "2016-10-25T07:00:00.000000Z"
      }
    },
    {
      "id": "46bb9ffe-2bbc-444d-977f-0f0e70b4b3ad",
      "departure_geo_point": {
        "latitude": 52.085165,
        "longitude": 5.116112
      },
      "arrival_geo_point": {
        "latitude": 52.334198,
        "longitude": 4.85967
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "ae228334-9d73-4971-8091-102c8ad85ed8",
      "community_id": "66f7b084-276d-444f-a376-b026a54e5b81",
      "created": "2016-10-24T12:19:54.106563Z",
      "modified": "2016-10-24T12:19:54.106585Z",
      "as_driver": true,
      "as_passenger": true,
      "extra": {
        "This works": "Well in the pattern API μService"
      },
      "travel_time": 2945.03455714128,
      "travel_distance": 32722.6061904587,
      "pattern_id": "73678a72-8764-4259-aff0-ffbefb6b2709",
      "departure_time": {
        "max": "2016-10-31T10:00:00.000000Z",
        "min": "2016-10-31T08:00:00.000000Z"
      }
    }
  ]
}
```
