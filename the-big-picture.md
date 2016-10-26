## Read Before Continue

###All request headers must contain `apikey` field.

## Glossary

Keywords : `Rideshare`, `Travel-intent-pattern`, `Travel-intent`

#### **Travel-intent**
Travel intent is a 'desire to move from A to B in a with a time window placed on either the departure or the arrival'.  You can either create your own travel-intent or you can let a travel-intent-pattern generate it for you.

###### *Example 1: User wants to arrive at work between 08:00 - 08:30. He/she can drive. So conceptually he/she can be a passenger or a driver. We can create our Travel-intent as follows:*

```
....
"arrival_time": {
  "max": "2016-07-29T08:30:00Z",
  "min": "2016-07-29T08:00:00Z"
},
"as_driver" : true,
"as_passenger" : true
...
```

###### *Example 2: User wants to leave the work between 17:00 - 17:30. He/she can't drive. So he/she can only be a passenger. We can create our travel-intent as follows*
```
...
"departure_time": {
  "max": "2016-07-29T17:30:00Z",
  "min": "2016-07-29T17:00:00Z"
},
"as_driver" : false,
"as_passenger" : true
...
```

#### Travel-intent-pattern
It declares a pattern of intents with specific parameters. For example if a user has to be at work every weekdays between 08:00 - 08:30. Instead of creating 5 different travel-intents, we can create a travel-intent-pattern with the following parameters:

```
...
"propagation_period": 604800, /* One week in seconds */
"effective_date": "2016-07-29T10:11:18Z", /* This pattern is active from this date.*/
"rrule": "FREQ=WEEKLY;BYDAY=MO,TU,WE,TH,FR,SA,SU", /* Every week, MO,TU,WE,TH,FR,SA,SU.*/
"departure_time": {
  "max": "11:00:00",
  "min": "09:00:00"
}
...
```  

#### Rideshare

When two travel intents fulfill conditions set by the back end, the pair are considered to be a match. That means the 2 users represented by the 2 intents should share that ride. We then generate a rideshare which merges the information from the 2 intents into one entity. This new entity is called a rideshare. You can NOT create a rideshare by itself. However you can create 2 similar intents in a community and the system will automatically generate a rideshare from the 2 intents.

After rideshare is created, we have to know which user is passenger and which user is the driver. Our system will assign `user_id`s as a `passenger_id` and `driver_id` according to their part in the rideshare.


![C42 1037 Pattern To Rideshare System Flow](https://d16co4vs2i1241.cloudfront.net/uploads/tutorial_image/file/617688486664734569/f2ba058b40d2dfb072c68529f1a3388c0f5b61fe4ae78e089e35aff063e24d2a/column_sized_C42-1037_pattern_to_rideshare_system_flow.jpg)


####FIRST PIC

There is a Pattern in travel
- Driver A has to be at work between 09:00 - 09:15 every weekdays
- Driver B has to be at work between 08:45 - 09:00 / THU, FRI
- Passenger C has to be at work between
09:00 - 09:15 / THU,FRI

Not everybody can drive
- There are drivers
- There are passengers

####SECOND PIC

Travel Intent patterns create travel-intents
- Driver A has to be at work between 09:00 - 09:15 every weekdays:
- System automatically creates 5 separate individual travel intents.
- This intents will be used for rideshare matching system
- Travel intents can be created separately as well


####THIRD PIC

Matched travel intents will be suggested
- All rideshares will have a score between 0-1.
- Scoring system is a calculation of multiple factors which came from travel intents.
- Best suggestion for a user is the suggestion that has highest score.


####FORTH PIC
How rideshare suggestions will be accepted by users
- When a rideshare born, its state will be new.
- When rideshare is in new state; driver or passenger can accept or decline. If one of them declines in any situation, rideshare is declined and will be deleted.
- If both users are accept the rideshare, the rideshare is accepted.
