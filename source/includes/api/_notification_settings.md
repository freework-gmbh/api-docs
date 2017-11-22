# Users

## Show User Notification Settings
### GET /users/settings/notifications

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/users/84390fcc-adcb-4446-afc3-4a6f7edeb12f'
```

Retrieves the notification settings for the current user.
You need to provide a valid freework `access_token` in the request header.

> Response with Status 200:

```json
{
  "notification_settings": {
        "enabled": true,
        "morning": true,
        "evening": true,
        "weekdays": {
            "friday": true,
            "monday": true,
            "tuesday": true,
            "thursday": true,
            "wednesday": true
        }
    },
}
```

## Update User Notification Settings
### PATCH /users/settings/notifications

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request PATCH '$API_URL/users/84390fcc-adcb-4446-afc3-4a6f7edeb12f' \
     --data '{
       "push_notifications": {
        "enabled": true,
        "morning": true,
        "evening": false,
        "weekdays": {
            "friday": false,
            "monday": true,
            "tuesday": true,
            "thursday": true,
            "wednesday": false
        }
	}
     }'
```

Update the user notification settings with the attributes provided. Not provided attributes won't be updated.
You need to provide a valid freework `access_token` in the request header.

Allowed attributes are:

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
enabled | boolean |  | Sets the permission for sending notifications to the user.
morning | boolean |  | Sets the permission for sending notifications to the user in the morning.
evening | boolean |  | Sets the permission for sending notifications to the user in the evening.
weekdays | jsonb |  | Sets the permission for sending push notifications on each weekday.

> Response with Status 200:

```json
{
  "notification_settings": {
        "enabled": true,
        "morning": true,
        "evening": true,
        "weekdays": {
            "friday": true,
            "monday": true,
            "tuesday": true,
            "thursday": true,
            "wednesday": true
        }
    },
}
```
