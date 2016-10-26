
##### GET /api/rideshare/v1/rideshare/
###### Example response
```
  "meta_data":{  
      "count":48,
      "limit":10,
      "offset":0
  },
  "data":[  
    {  
       "id":"your-generated-version-4-UUID",
       "travel_stops":[  
          {  
             "geo_point":{  
                "latitude":52.43870169,
                "longitude":4.81691348
             },
             "time_span":{  
                "max":"2016-10-19T15:30:00Z",
                "min":"2016-10-19T14:45:00Z"
             }
          },
          {  
             "geo_point":{  
                "latitude":52.43870169,
                "longitude":4.81691348
             },
             "time_span":{  
                "max":"2016-10-19T15:30:00Z",
                "min":"2016-10-19T14:45:00Z"
             }
          },
          {  
             "geo_point":{  
                "latitude":52.01339512,
                "longitude":4.36897508
             },
             "time_span":{  
                "max":"2016-10-19T16:54:21.959416Z",
                "min":"2016-10-19T16:09:21.959416Z"
             }
          },
          {  
             "geo_point":{  
                "latitude":51.99259675,
                "longitude":4.35860454
             },
             "time_span":{  
                "max":"2016-10-19T16:57:59.548702Z",
                "min":"2016-10-19T16:12:59.548702Z"
             }
          }
       ],
       "current_state":"new",
       "old_state":"empty",
       "community_id":"your-generated-version-4-UUID",
       "community_id":"your-generated-version-4-UUID",
       "created":"2016-10-12T15:35:04.938130Z",
       "modified":"2016-10-12T15:35:04.938165Z",
       "driver_id":"your-generated-version-4-UUID",
       "passenger_id":"your-generated-version-4-UUID",
       "driver_intent_id":"your-generated-version-4-UUID",
       "passenger_intent_id":"your-generated-version-4-UUID",
       "score":0.974690461708783,
       "travel_distance":58661.6522433057,
       "travel_time":5279.54870189751,
       "driver_intent_travel_distance":58576.3920042925,
       "driver_intent_travel_time":5271.87528038633,
       "passenger_intent_travel_distance":56243.9935131845,
       "passenger_intent_travel_time":5061.9594161866,
       "extra":null
    },
    {  },
    {  },
    {  },
    {  },
    {  },
    {  },
    {  },
    {  },
    {  }
  ]
```
###### Get - Rideshare Query-params

| Name  | Type | Example   | Description |
| :------------- | :------------- | :------------- | :------------- |
|`date_0='from'&date_1='till'` | `YYYY-MM-DDThh:mm:ss.ssssssZ` |  "/?date_0=2016-09-19T00:00:00Z&date_1=2016-09-20T00:00:00"  | Filters rideshares between a date range. To get all the rideshares from specific date to infinity you still have to provide a huge `date_1`. Query wont work if both `date_0` and `date_1` are not present.|
|`current_state` | `string` |  "/?current_state=deleted"|  Filters rideshares by current_state (See states for options)|
|`old_state` | `string` |  "/?old_state=new"| Filters rideshares by old_state (See states for options)|
|`community_id` | `string` |  "/?community_id=your-generated-version-4-UUID"| Filters rideshares by `community_id`|
|`driver_id` | `string` |  "/?driver_id=some-user-id-which-is-driver"| Filters rideshares by `driver_id`|
|`passenger_id ` | `string`|  "/?passenger_id=some-user-id-which-is-passenger"| Filters rideshares by `passenger_id`|
|`passenger_intent_id` | `string`|  "/?passenger_intent_id=some-passenger-intent-id"| Filters rideshares by `passenger_intent_id`|
|`driver_intent_id` | `string`|  "/?driver_intent_id=some-driver-intent-id"|Filters rideshares by `driver_intent_id`|

  * States:
    * new
    * driver_accepted
    * passenger_accepted
    * accepted
    * declined
    * deleted

![State Flow](assets/state_machine.png)

###### Examples Combined

| Name  |  Example   |
| :------------- | :------------- |
|"by date range and community", | "/?community_id=your-generated-version-4-UUID&date_0=2016-09-19T00:00:00Z&date_1=2016-09-20T00:00:00"
|"user as passenger rideshares in date range", | "/?passenger_id=some-user-id-which-is-passenger&date_0=2016-09-19T00:00:00Z&date_1=2016-09-20T00:00:00&current_state=new"



##### GET /api/rideshare/v1/rideshare/{id}/
###### Example response
```
{  
   "meta_data":{  

   },
   "data":[  
      {  
         "id":"your-generated-version-4-UUID",
         "travel_stops":[  
            {  
               "geo_point":{  
                  "latitude":52.43870169,
                  "longitude":4.81691348
               },
               "time_span":{  
                  "max":"2016-10-19T15:30:00Z",
                  "min":"2016-10-19T14:45:00Z"
               }
            },
            {  
               "geo_point":{  
                  "latitude":52.43870169,
                  "longitude":4.81691348
               },
               "time_span":{  
                  "max":"2016-10-19T15:30:00Z",
                  "min":"2016-10-19T14:45:00Z"
               }
            },
            {  
               "geo_point":{  
                  "latitude":52.01339512,
                  "longitude":4.36897508
               },
               "time_span":{  
                  "max":"2016-10-19T16:54:21.959416Z",
                  "min":"2016-10-19T16:09:21.959416Z"
               }
            },
            {  
               "geo_point":{  
                  "latitude":51.99259675,
                  "longitude":4.35860454
               },
               "time_span":{  
                  "max":"2016-10-19T16:57:59.548702Z",
                  "min":"2016-10-19T16:12:59.548702Z"
               }
            }
         ],
         "current_state":"new",
         "old_state":"empty",
         "community_id":"your-generated-version-4-UUID",
         "created":"2016-10-12T15:35:04.938130Z",
         "modified":"2016-10-12T15:35:04.938165Z",
         "driver_id":"your-generated-version-4-UUID",
         "passenger_id":"your-generated-version-4-UUID",
         "driver_intent_id":"your-generated-version-4-UUID",
         "passenger_intent_id":"your-generated-version-4-UUID",
         "score":0.974690461708783,
         "travel_distance":58661.6522433057,
         "travel_time":5279.54870189751,
         "driver_intent_travel_distance":58576.3920042925,
         "driver_intent_travel_time":5271.87528038633,
         "passenger_intent_travel_distance":56243.9935131845,
         "passenger_intent_travel_time":5061.9594161866,
         "extra":null
      }
   ]
}
```
##### GET /api/rideshare/v1/rideshare/{id}/state-diagram/
###### Example response
![State Flow](assets/state_machine.png)
##### GET /api/rideshare/v1/version/
###### Example response
`Status: 200 OK`

##### GET /api/rideshare/v1/health-check/
###### Example response
`Status: 200 OK`
##### POST /api/rideshare/v1/rideshare/{id}/actions/
  * Body:
    * ```
      {
        "user_id": "your-generated-version-4-UUID",
        "action": "accept"
      }```
    * ```
      {
        "user_id": "your-generated-version-4-UUID",
        "action": "decline"
      }```

###### Example response

```
{
  "status_code": 400,
  "detail": "Can't trigger event accept from state accepted!"
}
```

```
{
  "meta_data": {},
  "data": [
    {
      "id": "your-generated-version-4-UUID",
      "travel_stops": [
        {
          "geo_point": {
            "latitude": 52.011021,
            "longitude": 4.336688
          },
          "time_span": {
            "max": "2016-10-24T16:55:42.828720Z",
            "min": "2016-10-24T15:55:47.739720Z"
          }
        },
        {
          "geo_point": {
            "latitude": 52.051067,
            "longitude": 4.406224
          },
          "time_span": {
            "max": "2016-10-24T17:05:28.896633Z",
            "min": "2016-10-24T16:05:33.807633Z"
          }
        },
        {
          "geo_point": {
            "latitude": 52.165051,
            "longitude": 4.500659
          },
          "time_span": {
            "max": "2016-10-24T17:26:47.975000Z",
            "min": "2016-10-24T16:26:52.886000Z"
          }
        },
        {
          "geo_point": {
            "latitude": 52.165051,
            "longitude": 4.500659
          },
          "time_span": {
            "max": "2016-10-24T17:26:47.975000Z",
            "min": "2016-10-24T16:26:52.886000Z"
          }
        }
      ],
      "current_state": "driver_accepted",
      "old_state": "new",
      "community_id": "your-generated-version-4-UUID",
      "created": "2016-10-24T09:26:11.617061Z",
      "modified": "2016-10-24T09:37:15.348750Z",
      "driver_id": "your-generated-version-4-UUID",
      "passenger_id": "your-generated-version-4-UUID",
      "driver_intent_id": "your-generated-version-4-UUID",
      "passenger_intent_id": "your-generated-version-4-UUID",
      "score": 0.80624180446049,
      "travel_distance": 20723.8475495196,
      "travel_time": 1865.14627945676,
      "driver_intent_travel_distance": 20453.107835157,
      "driver_intent_travel_time": 1840.77970516413,
      "passenger_intent_travel_distance": 14211.9818493766,
      "passenger_intent_travel_time": 1279.07836644389,
      "extra": null
    }
  ]
}
```

##### DELETE /api/rideshare/v1/rideshare/{id}/
`204 No Content`
