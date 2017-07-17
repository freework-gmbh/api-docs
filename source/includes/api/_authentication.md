# Authentication

API clients receive an opaque access token, to be used in all subsequent requests (HTTP header). The access token times out after a pre-defined number of seconds. Once this time-out has occurred, the client must acquire a new access token by using the opaque refresh token it received together with the access token (or re-authenticate from scratch).

Before the client receives its tokens, the user has to authenticate successfully by providing valid credentials, using one of the following auth methods:

* **Freework account**: Login via email address and password
* **Linkedin Signin**: The user has to grant Freework access to his/her profile

## Registration
### POST /users/registration

```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users' \
     --data '{
       "user": {
         "email": "jane@example.com",
         "last_name": "Cruz",
         "password": "secret"
       }
     }'
```

Sign up for a Freework account. This endpoint is public (i.e. it does not require a Freework `access_token`).
However you need to provide a valid **client id** in the request header. Each of the apps (Android and iOS) have
their own `Client-ID` as a secret. The Freework API checks if the provided `Client-ID` is among the allowed Client-IDs.

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": null,
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
  }
}
```


### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
email | string | x | has to be a valid not taken email address
last_name | string | x | User's last name
password  | string | x | Users password of choice


### Errors
Status	| Key | Description
----------|------|-----------|----------
422 | email_taken | Account with this email address already exists


## Sign In
### POST /users/sessions/sign_in

```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users/sessions/sign_in' \
     --data '{
       "user": {
         "email": "jane@example.com",
         "password": "secret"
       }
     }'
```

Sign in with a Freework account. This endpoint is public (i.e. it does not require a Freework `access_token`).
However you need to provide a valid **Client-ID* in the request header. Each of the apps (Android and iOS) have
their own `Client-ID` as a secret. The Freework API checks if the provided `Client-ID` is among the allowed Client-IDs.

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": null,
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
email | string | x | has to be the email address of the account
password  | string | x | Password of the account


## Sign In with LinkedIn
### POST /users/linkedin/sign_in

```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users/sessions/sign_in' \
     --data '{
       "access-token": "some-linkedin-access-token",
       "mobile-sdk": true
     }'
```

Sign in with a LinkedIn account. This endpoint is public (i.e. it does not require a Freework `access_token`).
User needs to permit Freework to access their LinkedIn profile. Afterwards the linkedin 'access_token' is traded for a freework 'access_token'

However you need to provide a valid **Client-ID* in the request header. Each of the apps (Android and iOS) have
their own `Client-ID` as a secret. The Freework API checks if the provided `Client-ID` is among the allowed Client-IDs.

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": null,
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
access_token | string | x | has to be a not expired linkedin access_token
mobile_sdk  | boolean | x | Was the access token aquired with the linkedin mobile sdk or using the web auth flow.


## Refresh
### POST /users/sessions/refresh

Freework access token are short lived. Once a access token expires the client can either
sign in again or use their refresh token to aquire a new access_token (recommended).
Access tokens have an expire date long enough in the future (90 days).


```shell
curl --header 'Client-ID: Client-ID of app' \
     --header 'Content-Type: application/json' \
     --request POST '$API_URL/users/sessions/refresh' \
     --data '{
        "refresh_token": "some-freework-refresh-token"
     }'
```

> Response with Status 200:

```json
{
  "user": {
      "id": "84390fcc-adcb-4446-afc3-4a6f7edeb12f",
      "email": "jane@example.com",
      "first_name": null,
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
refresh_token | string | x | has to be a valid not expired refresh token
