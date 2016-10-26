##### GET /api/travel-intent/v1/travel-intent/
###### Example response
```
{
  "meta_data": {
    "count": 29189,
    "limit": 10,
    "offset": 0
  },
  "data": [
    {
      "id": "your-generated-version-4-UUID",
      "departure_geo_point": {
        "latitude": 52.011021,
        "longitude": 4.336688
      },
      "arrival_geo_point": {
        "latitude": 52.165051,
        "longitude": 4.500659
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "your-generated-version-4-UUID",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-08-24T09:28:43.593558Z",
      "modified": "2016-08-24T09:28:43.593582Z",
      "as_driver": true,
      "as_passenger": true,
      "extra": {
        "This intent is from": "driver"
      },
      "travel_time": 1840.77970516413,
      "travel_distance": 20453.107835157,
      "pattern_id": null,
      "arrival_time": {
        "max": "2016-08-24T17:28:43.077000Z",
        "min": "2016-08-24T16:28:43.076000Z"
      }
    },
    {...},
    {...},
  ]
}
```
###### GET - Travel Intent Query-params

| Name  | Type | Example   | Description |
| :------------- | :------------- | :------------- | :------------- |
| `ids` | `string` | `/?ids=some-travel-intent-id,some-travel-intent-id`| Filters travel intents by more than one id (can be seperated with commas) |
| `ids` | `string` | `/?ids=some-travel-intent-id,some-travel-intent-id`| Filters travel intents by more than one id (can be seperated with commas) |
| `user_id` | `string` | `/?user_id=some-user-id`| Filters travel intents by user_id|
| `user_id` | `string` | `/?user_id=some-user-id`| Filters travel intents by user_id|
| `by community_id` | `string` | `/?community_id=your-generated-version-4-UUID`| Filters travel intents by community_id|
| `by community_id` | `string` | `/?community_id=your-generated-version-4-UUID`| Filters travel intents by community_id|
| `by pattern_id` | `string` | `/?pattern_id=some-pattern-id`| Filters travel intents by pattern_id|
| `by pattern_id` | `string` | `/?pattern_id=some-pattern-id`| Filters travel intents by pattern_id|
| `date range` | `YYYY-MM-DDThh:mm:ss.ssssssZ` | `/?date_0=2016-08-02T08:00:00Z&date_1=2016-08-08T08:00:00Z`| Filters travel intents by looking for intents from within a specific date range. The filter will work with either `date_0` or `date_1` or both.|
| `date range` | `YYYY-MM-DDThh:mm:ss.ssssssZ` | `/?date_0=2016-08-02T08:00:00Z&date_1=2016-08-08T08:00:00Z`| Filters travel intents by looking for intents from within a specific date range. The filter will work with either `date_0` or `date_1` or both.|

==== EXAMPLES COMBINED

| Name  | Example   |
| :------------- | :------------- |
| "by Intent id, pattern id, user_id and community_id", | "/?ids=some-intent-id&user_id=some-user-id&community_id=your-generated-version-4-UUID"|
| "by pattern_id and time filter", | "/?pattern_id=some-pattern-id&date_0=2016-08-02T08:00:00Z&date_1=2016-08-08T08:00:00Z"|

##### GET /api/travel-intent/v1/health-check/
###### Example response
`200 OK`
##### GET /api/travel-intent/v1/travel-intent/{id}/

```
{
  "meta_data": {},
  "data": [
    {
      "id": "your-generated-version-4-UUID",
      "departure_geo_point": {
        "latitude": 52.011021,
        "longitude": 4.336688
      },
      "arrival_geo_point": {
        "latitude": 52.165051,
        "longitude": 4.500659
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "your-generated-version-4-UUID",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-10-24T08:52:19.158132Z",
      "modified": "2016-10-24T08:52:19.158167Z",
      "as_driver": true,
      "as_passenger": true,
      "extra": {
        "This intent is from": "driver or passenger"  
      },
      "travel_time": 1840.77970516413,
      "travel_distance": 20453.107835157,
      "pattern_id": null,
      "arrival_time": {
        "max": "2016-10-24T16:53:00.314000Z",
        "min": "2016-10-24T15:53:00.314000Z"
      }
    }
  ]
}
```

##### GET /api/travel-intent/v1/swagger/

##### POST /api/travel-intent/v1/travel-intent/
  * Body:
```
  {
    "user_id":"your-generated-version-4-UUID",
    "community_id":"your-generated-version-4-UUID",
    "departure_geo_point": {
      "latitude": 52.002636563,
      "longitude": 4.4545484684
    },
    "arrival_geo_point": {
      "latitude": 52.002636563,
      "longitude": 4.4545484684
    },
    "extra": {"This intent is from":"some user"},    
    "timezone": "Europe/Amsterdam",
    "as_driver":true,
    "as_passenger":true,
    "arrival_time": {
      "max": "2016-07-29T12:00:00Z",
      "min": "2016-07-29T10:00:00Z"
    }
  }
```

###### Post - Travel-intent fields
| Name  | Type | Example   |  Required | Description |
| :------------- | :------------- | :------------- | :------------- | :------------- |
| `user_id` | `string` | "b0ae803a-affa-4198-8b77-cf8ceeb6758d" | true | Each travel_intent can be related to one and only one user_id. (1-N relationship respectively)| $$$ Maybe also show the fact that intents to rideshares also have a 1-N relationship? Dunno if this is teh right place for it though
| `community_id` | `string` | "b0ae803a-affa-4198-8b77-cf8ceeb6758d" | true | Filter travel intents from a community |
| `community_id` | `string` | "b0ae803a-affa-4198-8b77-cf8ceeb6758d" | true | Filter travel intents from a community |
| `departure_geo_point` |  `JSONObject` | example | true | Travel Intents has departure locations which has its own `latitude`, `longitude`. |
| `arrival_geo_point` | `JSONObject` | example | true | Travel Intents has departure locations which has its own `latitude`, `longitude`. |
| `timezone` | `string` | "Europe/Amsterdam" | true | Check `IANA timezone list` for all possible timezones |
| `extra` | `JSONObject` | {"AnyJsonKey":"AnyJsonParam"} | false | You can send extra data to the BE for later use|
| `as_driver` | `boolean` | true | true | Is the user which is has provided as `user_id` can be a driver for this intent  |
| `as_passenger` | `boolean` | true | true | Is the user which is has provided as `user_id` can be a passenger for this intent |
| `departure_time` | `JSONObject` | example | interchangeable with `arrival_time` | You can only provide either `departure_time` or `arrival_time`. Otherwise you will get `400`. Our backend takes supplied param (`departure_time` or `arrival_time` as you provided) and try to find a shareable ride accordingly. |
| `arrival_time` | `JSONObject` | example | interchangeable with `departure_time` | You can only provide either `departure_time` or `arrival_time`. |

```
"departure_geo_point": {
  "latitude": 52.002636563,
  "longitude": 4.4545484684
},
```
```
"arrival_time": {
  "max": "2016-07-29T12:00:00Z",
  "min": "2016-07-29T10:00:00Z"
}
```
###### Example response
`201 Created`
```
{
  "meta_data": {},
  "data": [
    {
      "id": "your-generated-version-4-UUID",
      "departure_geo_point": {
        "latitude": 52.011021,
        "longitude": 4.336688
      },
      "arrival_geo_point": {
        "latitude": 52.165051,
        "longitude": 4.500659
      },
      "current_state": "new",
      "old_state": "empty",
      "user_id": "your-generated-version-4-UUID",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-10-24T08:58:35.389017Z",
      "modified": "2016-10-24T08:58:35.389039Z",
      "as_driver": true,
      "as_passenger": true,
      "extra": {
        "This intent is from": "driver"
      },
      "travel_time": 1840.7797051641314,
      "travel_distance": 20453.107835157014,
      "pattern_id": null,
      "arrival_time": {
        "max": "2016-10-24T16:59:16.532000Z",
        "min": "2016-10-24T15:59:16.532000Z"
      }
    }
  ]
}
```

##### DELETE /api/travel-intent/v1/travel-intent/{id}/
###### Example response
`204 No Content`
