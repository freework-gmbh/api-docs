## Create Customer
### PUT /customers

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/customers' \
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

Create a new customer with the attributes provided.
You need to provide a valid freework `access_token` in the request header.

Allowed attributes are:

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
name | string | x | has to be a valid string
color | string | x  | has to be a valid color hex code
address | json | | ignore for now
currency | string | x | has to be a valid currency code(ISO 4217)
hourly_rate | numeric | has to be a valid numeric value (eg. 21.5)

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

