---
title: API Reference

language_tabs:
  - shell
  - ruby
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Freework API!

This api is used for all of our mobile app. We try to keep them as up to date as possible.
Please let us know if something is missing or if there are any bugs at <tech@freework.io>

## General information

```shell
export API_URL="api.freework.io"
```

```ruby
API_URL = "api.freework.io"
```

The api base url will be referenced as `API_URL` in the rest of the documentation.
It differs depending on environment (e.g. edge or production).

> `Content-Type: application/json`

Please always make sure to always send `Content-Type: application/json` in the header.


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
       "email": "jane@example.com",
       "last_name": "Cruz",
       "password": "secret"
       "password_confirmation": "secret"
     }'
```

Sign up for a Freework account. This endpoint is public (i.e. it does not require a Freework `access_token`).
However you need to provide a valid **client id** in the request header. Each of the apps (Android and iOS) have
their own `Client-ID` as a secret. The Freework API checks if the provided `Client-ID` is among the allowed Client-IDs.

### Attribute Defintions

Attribute	| Type | Mandatory |Definition
----------|------|-----------|----------
email | string | x | has to be a valid not taken email address
last_name | string | x | User's last name
password  | string | x | Users password of choice
password_confirmation | string | x | has to match password
