## Travel-intent-pattern

##### GET /api/travel-intent-pattern/v1/travel-intent-pattern/
###### Example response
```
{
  "meta_data": {
    "count": 988,
    "limit": 10,
    "offset": 0
  },
  "data": [
    {
      "id": "your-generated-version-4-UUID",
      "departure_geo_point": {
        "latitude": 52.00949901,
        "longitude": 4.35619812
      },
      "arrival_geo_point": {
        "latitude": 52.43870169,
        "longitude": 4.81691348
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "your-generated-version-4-UUID",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-10-17T08:36:20.313587Z",
      "modified": "2016-10-19T05:35:01.688176Z",
      "as_driver": false,
      "as_passenger": true,
      "timezone": "Europe/Amsterdam",
      "extra": null,
      "propagation_period": 604800,
      "propagated_until": "2016-11-02T05:35:01.686484Z",
      "effective_date": "2016-10-24T08:36:20.244536Z",
      "rrule": "FREQ=WEEKLY;BYDAY=WE;UNTIL=20161024T083921Z",
      "arrival_time": {
        "max": "08:15:00",
        "min": "07:30:00"
      }
    },
    {...},
    {...}
  ]
}
```
###### Get - Travel Intent Pattern Query-params

| Name  | Type | Example   | Description |
| :------------- | :------------- | :------------- | :------------- |
|`user_id`,  | `string` | `/?user_id=some-user-id`| Filter travel intent patterns by user_id |
|`community_id`,  | `string` | `/?community_id=your-generated-version-4-UUID`| Filter travel intent patterns by community_id |
|`ids`,  | `string` | `/?ids=some-pattern-id`| Filter travel intent patterns by user_id (can be seperated with commas) |

  ==== EXAMPLES COMBINED

| Name  | Example   |
| :------------- | :------------- |
|"by pattern id, user_id and community_id",  | "/?ids=some-pattern-id&user_id=some-user-id&community_id=your-generated-version-4-UUID"|

##### GET /api/travel-intent-pattern/v1/travel-intent-pattern/{id}/
###### Example response
```
{
  "id": "your-generated-version-4-UUID",
  "departure_geo_point": {
    "latitude": 52.00949901,
    "longitude": 4.35619812
  },
  "arrival_geo_point": {
    "latitude": 52.43870169,
    "longitude": 4.81691348
  },
  "current_state": "new",
  "old_state": "empty",
  "user_id": "your-generated-version-4-UUID",
  "community_id": "your-generated-version-4-UUID",
  "created": "2016-10-17T08:36:20.313587Z",
  "modified": "2016-10-19T05:35:01.688176Z",
  "as_driver": false,
  "as_passenger": true,
  "timezone": "Europe/Amsterdam",
  "extra": null,
  "propagation_period": 604800,
  "propagated_until": "2016-11-02T05:35:01.686484Z",
  "effective_date": "2016-10-24T08:36:20.244536Z",
  "rrule": "FREQ=WEEKLY;BYDAY=WE;UNTIL=20161024T083921Z",
  "arrival_time": {
    "max": "08:15:00",
    "min": "07:30:00"
  }
}
```
##### GET /api/travel-intent-pattern/v1/health-check/
`204 No Content`
##### POST /api/travel-intent-pattern/v1/travel-intent-pattern/
  * Body:

```
    "user_id":"your-generated-version-4-UUID",
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
    "rrule": "FREQ=WEEKLY;BYDAY=MO,TU,WE,TH,FR,SA,SU",
    "propagation_period":604800,
    "departure_time": {
      "max": "11:00:00",
      "min": "09:00:00"
    },
    "arrival_time": null
  }
```

###### Post - Travel-intent-pattern fields
| Name  | Type | Example   |  Required | Description |
| :------------- | :------------- | :------------- | :------------- | :------------- |
|`user_id` | `string` | "b0ae803a-affa-4198-8b77-cf8ceeb6758d" | true | Every Travel-intent-pattern paired with one and only one unique user_id. (1-N relationship) |
|`community_id` | `string` | "b0ae803a-affa-4198-8b77-cf8ceeb6758d" | true | Travel-intent-patterns belongs to a community |
|`departure_geo_point` | `JSONObject` | example | true | Travel-intent-patterns has departure locations which has its own `latitude`, `longitude`. |
|`arrival_geo_point` | `JSONObject` | example | true | Travel-intent-patterns has departure locations which has its own `latitude`, `longitude`. |
|`timezone` | `string` | "Europe/Amsterdam" | true | Check `IANA timezone list` for all possible timezones |
|`extra` | `JSONObject` | {"AnyJsonKey":"AnyJsonParam"} | true | You can send extra data to the BE for later use |
|`as_driver` | `boolean` | true | true | Is the user which is has provided as `user_id` can be a driver for this intent-pattern ? |
|`as_passenger` | `boolean` | false | true | Is the user which is has provided as `user_id` can be a passenger for this intent-pattern ? |
|`rrule` | `string` | FREQ=WEEKLY;BYDAY=MO,TU,WE,TH,FR,SA,SU | true | Travel intent PATTERN rule. See https://www.textmagic.com/free-tools/rrule-generator. |
|`effective_date` | `string` | "2016-07-29T10:11:18" | true | When the rrule becomes active |
|`propagation_period` | `number` | 604800 | true | how long `rrule` pattern can be able to generate travel-intents (In seconds) |
| `departure_time` | `JSONObject` | example | interchangeable with `arrival_time` | You can only provide either `departure_time` or `arrival_time`. Otherwise you will get `400`. Our backend takes supplied param (`departure_time` or `arrival_time` as you provided) and try to find a shareable ride accordingly. |
| `arrival_time` | `JSONObject` | example | interchangeable with `departure_time` | You can only provide either `departure_time` or `arrival_time`. |


###### Example response
```
{
  "meta_data": {},
  "data": [
    {
      "id": "your-generated-version-4-UUID",
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
      "user_id": "your-generated-version-4-UUID",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-10-24T09:49:29.389728Z",
      "modified": "2016-10-24T09:49:29.389751Z",
      "as_driver": true,
      "as_passenger": true,
      "timezone": "Europe/Amsterdam",
      "extra": {
        "This works": "Well in the pattern API μService"
      },
      "propagation_period": 604800,
      "propagated_until": null,
      "effective_date": "2016-07-29T10:11:18Z",
      "rrule": "FREQ=WEEKLY;BYDAY=MO,TU,WE,TH,FR,SA,SU",
      "departure_time": {
        "max": "11:00:00",
        "min": "09:00:00"
      }
    }
  ]
}
```


##### DELETE /api/travel-intent-pattern/v1/travel-intent-pattern/{id}/
###### Example response
`204 No Content`
