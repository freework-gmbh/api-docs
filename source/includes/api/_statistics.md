# Statistics

## Show Statistics
### GET /statistics

```shell
curl --header 'Authorization: Bearer: some-freework-access-token' \
     --header 'Content-Type: application/json' \
     --request GET '$API_URL/statistics'
```

Retrieve some app usage information about the current user.
You need to provide a valid freework `access_token` in the request header.

> Response with Status 200:

```json
{
  "statistics": {
            "total_days_since_user_created": 123,
            "total_tasks": 34,
            "total_tracked_seconds": 30585600,
          },
}
```
