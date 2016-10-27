

### 200 - OK

Everything worked as expected.

---
### 201 - No Content

Created an Entity and everything worked as expected.

---
### 204 - No Content

Deleted an Entity and everything worked as expected.

---

### 400 Bad request


* Missing a required parameter

    ```
    {
      "user_id": [
        "This field is required."
      ],
      "status_code": 400
    }
    ```
* Wrong value for a parameter

    ```
    {
      "user_id": [
        "\"loremipsum\" is not a valid UUID."
      ],
      "status_code": 400
    }
    ```
* Supplied both of the interchangeable params (`arrival_time` & `departure_time`)

    ```
    {
      "non_field_errors": [
        "Invalid: Only arrival or departure min or max times can be defined"
      ],
      "status_code": 400
    }
    ```

* Made a request against our system logic check **[State Diagram](#state-diagram)**:

    Trying to accept a rideshare after its been declined:

    ```
    {
      "status_code": 400,
      "detail": "Can't trigger event accept from state declined!"
    }
    ```

---


### 401 Unauthorized

`apikey` field must be present in all requests.

```
{
  "message": "No API Key found in headers, body or querystring"
}
```

---

### 404 - Not Found

* Hit an non-existent url

    ```
    {
      "request_path": "/api/rideshare-lorem/v1/rideshare/",
      "message": "API not found with these values",
      "request_host": [
        "dev04.c42.io"
      ]
    }
    ```

* Trying to delete an entity that doesn't exist (DELETE /rideshare/v1/rideshare/loremipsum)

    ```
    {
      "status_code": 404,
      "detail": "Not found."
    }
    ```

---
### 500, 502, 503, 504 - Server Errors

Something went wrong on Calendar42's end.
