# Oauth Authentication

API clients receive an opaque access token, to be used in all subsequent requests (HTTP header). The access token times out after a pre-defined number of seconds. Once this time-out has occurred, the client must acquire a new access token by using the opaque refresh token it received together with the access token (or re-authenticate from scratch).

Before the client receives its tokens, the user has to authenticate successfully by providing valid credentials, using one of the following auth methods:

## Logout
### POST /users/sessions/logout

```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users/sessions/sign_in' \
     --data '{
       "push_notifications":{
         "player_id": "a4860d5c-ff09-4566-b54f-e7d9e4d395b9"
       }
     }'
```

Removes the user device from the database in order to stop it from receiving future notifications on that device.

> Response with Status 200:

```json
{}
```


### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
player_id  | uuid |  | Device player_id from onesignal

## Sign in with Google
### POST /google/sign_in

```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users/sessions/sign_in' \
     --data '{
       "locale": "en-US",
       "user": {
         "access_token":"ya29.GlvnBBSdrkRO5NfP982U-Pjqj13wCS3FphCh5iywhMRhbRXogWLEYI3S7hCiBel-92-wPSWIY8X5i42Ua2qPbTYhuI34l5_8XoKN0AXFj0h1Q7RHy_cIuO3vdxoQ",
      	 "email": "penelope@freework.io",
      	 "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjRlZWM5NjBhNmQ1MGE3NG",
      	 "name": "Penelope Cruz",
      	 "photo": "https://lh3.googleusercontent.com/-30B4Huhyzv8/AAAAAAAAAAI/AAAAAAAAAAA/ACnBePao1bMSKPUdxnwn/s120/photo.jpg",
         "push_notifications":{
           "player_id": "a4860d5c-ff09-4566-b54f-e7d9e4d395b9",
           "device_token": "a4860d5c-ff09-4566-b54f-e7d9e4d395b9"
         }
      	}
       }
     }'
```

Sign in with a Google account. This endpoint is public (i.e. it does not require a Freework `access_token`).
User needs to permit Freework to access their Google profile. Afterwards the google 'access_token' is traded for a freework 'access_token'

However you need to provide a valid *Client-ID* in the request header. Each of the apps (Android and iOS) have
their own `Client-ID` as a secret. The Freework API checks if the provided `Client-ID` is among the allowed Client-IDs.

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
  "meta": {
      "access_token": "some-freework-access-token",
      "expires_at": 1498416796,
      "refresh_token": "some-freework-refresh-token"
  }
}
```


### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
access_token | string | x | has to be a not expired google access_token
id_token  | string | x | token used to request information on google api
email | string | x | has to be a valid not taken email address
name | string | x | User's full name
photo | string | x | URI for the user google profile picture
player_id  | uuid |  | Device player_id from onesignal
device_token  | uuid |  | Device push token from onesignal
