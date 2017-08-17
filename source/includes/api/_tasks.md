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
          "starts_at": "2017-07-21T08:22:56Z",
          "hourly_rate": "25.5",
          "currency": "EUR"
      }
     }'
```

Creates a new task with the attributes provided.
You need to provide a valid freework `access_token` in the request header.

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | x | has to be an existing customer of the user
description | string | x  | has to be a valid description
starts_at | string | x | Date when the task starts (iso8601 format)
ends_at | string | | Date when the task ends (iso8601 format)
hourly_rate | numeric | | has to be a valid numeric value (eg. 21.5)
currency | string | x | has to be a valid currency code(ISO 4217)

> Response with Status 200:

```json
{
  "task": {
    "id": "16886c8a-9175-459c-a550-1ea7297b296f",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "starts_at": "2017-07-21T08:22:56Z",
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
     --request GET '$API_URL/tasks?limit=3&starts_at[gte]=2017-08-10'
```

Returns all the tasks of the current user (limit is 100). The request must contain a valid freework `access_token` in the request header.

### Arguments

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | | has to be an existing customer of the user
limit | integer | | A value between 1..100 (default: 100)
starts_at | dictionary | | A dictionary describing an interval for the starts_at field
ends_at | dictionary | | A dictionary describing an interval for the ends_at field

### starts_at / ends_at dictionaries

Argument | Type | Mandatory |Definition
----------|------|-----------|----------
gte | string | | Return values where the field is after or equal to this timestamp.
lte | string | | Return values where the field is before or equal to this timestamp.


> Response with Status 200:

```json
[
  {
    "task": {
      "id": "35608a6e-048c-4f45-9848-362e1341e697",
      "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
      "description": "This is an example paragraph",
      "starts_at": "2017-07-21T08:22:56Z",
      "hourly_rate": "50.5",
      "currency": "USD"
    }
  },
  {
    "task": {
      "id": "ae32be60-14a8-4ce3-98e8-02471b0201d0",
      "customer_id": "94c298b5-0e9c-4dbe-9f1d-cda0722aca49",
      "description": "This is another example paragraph",
      "starts_at": "2017-07-21T08:23:40Z",
      "hourly_rate": "25.5",
      "currency": "EUR"
    }
  }
]
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
A valid freework `access_token` is required on the header.

Allowed attributes are:

### Attribute Defintions

Attribute | Type | Mandatory |Definition
----------|------|-----------|----------
customer_id | uuid | | has to be an existing customer of the user
description | string | | has to be a valid description
starts_at | string | | Date when the task starts (iso8601 format)
ends_at | string | | Date when the task ends (iso8601 format)
hourly_rate | numeric | | has to be a valid numeric value (eg. 21.5)
currency | string | | has to be a valid currency code(ISO 4217)

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "starts_at": "2017-07-21T08:22:56Z",
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

> Response with Status 200:

```json
{
  "task": {
    "id": "35608a6e-048c-4f45-9848-362e1341e697",
    "customer_id": "fab3368d-7295-4e72-aedd-42906ce000e9",
    "description": "This is an example paragraph",
    "starts_at": "2017-07-21T08:22:56Z",
    "hourly_rate": "50.5",
    "currency": "USD"
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
    "starts_at": "2017-07-21T08:22:56Z",
    "hourly_rate": "50.5",
    "currency": "USD"
  }
}
```
