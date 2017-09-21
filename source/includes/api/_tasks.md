# Tasks

## Create Task
### POST /tasks

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/tasks' \
     --data '{
      "task": {
          "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
          "description": "This is an example paragraph",
          "started_at": "2017-07-21T08:22:56Z",
          "current_timer_started_at": "2017-07-21T08:22:56Z",
          "hourly_rate": "25.5",
          "currency": "EUR"
      }
     }'
```

Creates a new task with the attributes provided and starts tracking time for it.
You need to provide a valid freework `access_token` in the request header.

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | x | has to be an existing customer of the user
description | string | x  | has to be a valid description
started_at | string | x | Date when the task starts (iso8601 format)
ended_at | string | | Date when the task ends (iso8601 format)
current_timer_started_at | string | x | Date when the timer was started (iso8601 format)
hourly_rate | numeric | | has to be a valid numeric value (eg. 21.5)
currency | string | x | has to be a valid currency code(ISO 4217)

> Response with Status 200:

```json
{
  "task": {
    "id": "16886c8a-9175-459c-a550-1ea7297b296f",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": null,
    "current_timer_started_at": "2017-07-21T08:22:56Z",
    "tracked_duration": 0,
    "hourly_rate": "25.5",
    "currency": "EUR"
  }
}
```

## List Tasks
### GET /tasks

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/tasks?limit=3&started_at[gte]=2017-08-10'
```

Returns all the tasks of the current user (limit is 100). The request must contain a valid freework `access_token` in the request header.

### Arguments

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | | has to be an existing customer of the user
limit | integer | | A value between 1..100 (default: 100)
started_at | dictionary | | A dictionary describing an interval for the started_at field
ended_at | dictionary | | A dictionary describing an interval for the ended_at field
includes | string | | A string containing the entities to be included with the tasks, separated by comma. Avaliables includes are: `customer`.

### started_at / ended_at dictionaries

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
gte | string | | Return values where the field is after or equal to this timestamp.
lte | string | | Return values where the field is before or equal to this timestamp.


> Response with Status 200:

```json
{
  "tasks":
  [
    {
      "id": "35608a6e-048c-4f45-9848-362e1341e697",
      "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
      "description": "This is an example paragraph",
      "started_at": "2017-07-21T08:22:56Z",
      "ended_at": null,
      "current_timer_started_at": "2017-07-21T08:22:56Z",
      "tracked_duration": 0,
      "hourly_rate": "50.5",
      "currency": "USD"
    },
    {
      "id": "ae32be60-14a8-4ce3-98e8-02471b0201d0",
      "customer_id": "94c298b5-0e9c-4dbe-9f1d-cda0722aca49",
      "description": "This is another example paragraph",
      "started_at": "2017-07-21T08:23:40Z",
      "ended_at": null,
      "current_timer_started_at": "2017-07-21T08:22:56Z",
      "tracked_duration": 0,
      "hourly_rate": "25.5",
      "currency": "EUR"
    }
  ],
  "customers":
  [
    {
        "id": "94c298b5-0e9c-4dbe-9f1d-cda0722aca49",
        "name": "Example Inc",
        "color": "#cccccc",
        "currency": "EUR",
        "hourly_rate": "25.5"
    }
  ]
}
```

## Update Task
### PATCH /tasks/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/tasks/35608a6e-048c-4f45-9848-362e1341e697' \
     --data '{
      "task": {
          "hourly_rate": "50.5",
          "currency": "USD"
      }
     }'
```

Updates the task with the attributes provided, without changing the ones that are not included in the request.
If you update the `tracked_duration` field, this will cause the `ended_at` timestamp to change as to keep the
time tracking consistent.
A valid freework `access_token` is required on the header.

Allowed attributes are:

### Attribute Defintions

Attribute | Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | | has to be an existing customer of the user
description | string | | has to be a valid description
started_at | string | | Date when the task starts (iso8601 format)
ended_at | string | | Date when the task ends (iso8601 format)
tracked_duration | int | | Tracked interval, in seconds
hourly_rate | numeric | | has to be a valid numeric value (eg. 21.5)
currency | string | | has to be a valid currency code(ISO 4217)

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": null,
    "current_timer_started_at": "2017-07-21T08:22:56Z",
    "tracked_duration": 0,
    "hourly_rate": "50.5",
    "currency": "USD"
  }
}
```

## Read Task
### GET /tasks/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/tasks/35608a6e-048c-4f45-9848-362e1341e697'
```

Returns the task for this id. The task must belong to the current user, and the request must contain a valid freework `access_token` in the request header.

### Arguments

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
includes | string | | A string containing the entities to be included with the tasks, separated by comma. Avaliables includes are: `customer`.

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": null,
    "current_timer_started_at": "2017-07-21T08:22:56Z",
    "tracked_duration": 0,
    "hourly_rate": "50.5",
    "currency": "USD"
  },
  "customer": {
      "id": "fab3368d-7295-4e72-aedd-42906ce000e9",
      "name": "Example Inc",
      "color": "#cccccc",
      "currency": "EUR",
      "hourly_rate": "25.5"
  }
}
```

## Delete Task
### DELETE /tasks/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request DELETE '$API_URL/tasks/35608a6e-048c-4f45-9848-362e1341e697'
```

Deletes the task for this id. The task must belong to the current user, and the request must contain a valid freework `access_token` in the request header.

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": null,
    "current_timer_started_at": "2017-07-21T08:22:56Z",
    "tracked_duration": 0,
    "hourly_rate": "50.5",
    "currency": "USD"
  }
}
```

## Pause Task
### PATCH /tasks/:id/pause

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/tasks/35608a6e-048c-4f45-9848-362e1341e697' \
     --data '{
      "ended_at": "2017-08-16 15:50:03 UTC"
     }'
```

Pauses the timer for the selected task, updating the `ended_at` field with the provided timestamp, setting the `current_timer_started_at` to `nil` and automatically updates the `tracked_duration` field. The timer must be currently running (i.e. `current_timer_started_at` cannot be `nil`) for this request to succeed.
A valid freework `access_token` is required on the header.

Allowed attributes are:

### Attribute Defintions

Attribute | Type | Mandatory |Definition
----------|------|-----------|----------
ended_at | time | | a UTC timestamp not earlier than the time when the task was first started or the timer was last initiated.

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": "2017-07-21T08:23:56Z",
    "current_timer_started_at": null,
    "tracked_duration": 60,
    "hourly_rate": "50.5",
    "currency": "USD"
  }
}
```

## Resume Task
### PATCH /tasks/:id/start

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/tasks/35608a6e-048c-4f45-9848-362e1341e697' \
     --data '{
      "current_timer_started_at": "2017-08-16 15:50:03 UTC"
     }'
```

Resumes the timer for the selected task, updating the `current_timer_started_at` field with the provided timestamp. The timer must be currently stopped (i.e. `current_timer_started_at` equals to `nil`) for this request to succeed.
A valid freework `access_token` is required on the header.

Allowed attributes are:

### Attribute Defintions

Attribute | Type | Mandatory |Definition
----------|------|-----------|----------
current_timer_started_at | time | | a UTC timestamp not earlier than the time when the task was first started or the timer was last stopped.

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": "2017-07-21T08:23:56Z",
    "current_timer_started_at": "2017-07-21T08:24:56Z",
    "tracked_duration": 60,
    "hourly_rate": "50.5",
    "currency": "USD"
  }
}
```

## Current Task
### GET /tasks/current

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/tasks/current'
```

Returns the `task` that is currently running for the user, if any. A valid freework `access_token` is required on the header.

### Arguments

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
includes | string | | A string containing the entities to be included with the tasks, separated by comma. Avaliables includes are: `customer`.

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "started_at": "2017-07-21T08:22:56Z",
    "ended_at": null,
    "current_timer_started_at": "2017-07-21T08:22:56Z",
    "tracked_duration": 0,
    "hourly_rate": "50.5",
    "currency": "USD"
  },
  "customer": {
      "id": "fab3368d-7295-4e72-aedd-42906ce000e9",
      "name": "Example Inc",
      "color": "#cccccc",
      "currency": "EUR",
      "hourly_rate": "25.5"
  }
}
```

## Export tasks
### GET /tasks/exports/csv

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/tasks/exports/csv'
```

Generates a csv file containing the user's tasks information, and sends a email with the download link for the file.
The endpoint itself does not return any data other than the status code. If the user has already requested an export
in the last hour, the server returns a 406 error.

> Response with Status 200:

```json
{}
```
