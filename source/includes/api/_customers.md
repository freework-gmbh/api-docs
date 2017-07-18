# Customers

## Create Customer
### POST /customers

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/customers' \
     --data '{
        {
          "customer": {
            "name": "Example Inc",
            "currency": "EUR",
            "color": "#cccccc"
          }
        }
     }'
```

Creates a new customer with the attributes provided.
You need to provide a valid freework `access_token` in the request header.

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
name | string | x | has to be a valid string
color | string | x  | has to be a valid color hex code
address | json | | ignore for now
currency | string | x | has to be a valid currency code(ISO 4217)
hourly_rate | numeric | | has to be a valid numeric value (eg. 21.5)

> Response with Status 200:

```json
{
    "customer": {
        "id": "16886c8a-9175-459c-a550-1ea7297b296f",
        "name": "Example Inc",
        "address": {
            "line1": null,
            "line2": null,
            "line3": null,
            "postal_code": null,
            "city": null,
            "region": null,
            "country_code": null
        },
        "color": "#cccccc",
        "houry_rate": null
    }
}
```

## List Customers
### GET /customers

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/customers'
```

Returns all customers of the current user (limit is 100).
You need to provide a valid freework `access_token` in the request header.

> Response with Status 200:

```json
[
    {
        "customer": {
            "id": "94c298b5-0e9c-4dbe-9f1d-cda0722aca49",
            "name": "Freework",
            "address": {
                "line1": null,
                "line2": null,
                "line3": null,
                "postal_code": null,
                "city": null,
                "region": null,
                "country_code": null
            },
            "color": "#abcabc",
            "houry_rate": null
        }
    },
    {
        "customer": {
            "id": "ae32be60-14a8-4ce3-98e8-02471b0201d0",
            "name": "Example Inc",
            "address": {
                "line1": null,
                "line2": null,
                "line3": null,
                "postal_code": null,
                "city": null,
                "region": null,
                "country_code": null
            },
            "color": "#cccccc",
            "houry_rate": null
        }
    }
]
```

## Delete Customer
### DELETE /customers/:id

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request DELETE '$API_URL/customers/ae32be60-14a8-4ce3-98e8-02471b0201d0'
```

Deletes the customer with this id. It has to belong to the current user.
You need to provide a valid freework `access_token` in the request header.

> Response with Status 200 if Customer is deleted

> Response with Status 404 if Customer is not found
```

