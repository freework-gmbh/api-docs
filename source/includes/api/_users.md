# Users

## Show User
### GET /users/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/users/84390fcc-adcb-4446-afc3-4a6f7edeb12f'
```

Retrieve information about the user with a certain `id`.
However you need to provide a valid freework `access_token` in the request header.

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": "Jane",
      "last_name": "Cruz",
      "linkedin_id": null,
      "created_at": "2017-06-25 17:43:35 UTC",
      "updated_at": "2017-06-25 17:43:35 UTC",
      "phone": null,
      "address": {
          "line1": null,
          "line2": null,
          "line3": null,
          "postal_code": null,
          "city": null,
          "region": null,
          "country_code": null
      },
      "job_title": null,
      "picture_url": null
  },
}
```

## Update User
### PATCH /users/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/users/84390fcc-adcb-4446-afc3-4a6f7edeb12f' \
     --data '{
       "user": {
         "first_name": "Jane",
         "phone": "012345-67890123"
       }
     }'
```

Update the user with the attributes provided. Not provided attributes won't be updated.
However you need to provide a valid freework `access_token` in the request header.

Allowed attributes are:

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
first_name | string |  | has to be a valid string
last_name | string |  | has to be a valid string
email | string |  | has to be a valid email address
phone | string |  | has to be a valid phone number
job_title | string |  | has to be a valid string

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": "Jane",
      "last_name": "Cruz",
      "linkedin_id": null,
      "created_at": "2017-06-25 17:43:35 UTC",
      "updated_at": "2017-06-25 17:43:35 UTC",
      "phone": null,
      "address": {
          "line1": null,
          "line2": null,
          "line3": null,
          "postal_code": null,
          "city": null,
          "region": null,
          "country_code": null
      },
      "job_title": null,
      "picture_url": null
  },
}
```

