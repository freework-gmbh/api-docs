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
