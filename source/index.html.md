---
title: Freework API

language_tabs:
  - shell

toc_footers:
  - <a href='mailto:tech@freework.io'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - api/authentication
  - api/users
  - api/customers
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

The api base url will be referenced as `API_URL` in the rest of the documentation.
It differs depending on environment (e.g. edge or production).

> `Content-Type: application/json`

Please always make sure to always send `Content-Type: application/json` in the header.
