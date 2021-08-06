---
title: abbr.ninja API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>
  - <a href="https://abbr.ninja/">Go back to abbr.ninja</a>

includes:
  - http_status_codes

search: true

code_clipboard: true
---

# Introduction

This document describes the API available. You agree to abide by the terms and conditions by interacting with the API.

Base URL: `https://api.abbr.ninja/api/v1`

<!-- # Rate Limit

Endpoint | Request / minute
-------- | ----------------
`/retrieve` | 120
`/shorten` | 20

`429 Too Many Requests` will be returned if you hit the rate limit. See the [HTTP Codes](#http-status-codes) section for other error codes. -->

# Create/Retrieve URI

## Shorten URI

```shell
curl "https://api.abbr.ninja/api/v1/shorten" \
  -X POST -H "Content-Type:application/json" \
  -d '{"uri":"https://example.com/longlongstuff"}'
```

> Response:

> 200 OK:

```json
{
  "id": "aJKjknR",
  "html_safe_uri": "https://example.com/longlongstuff",
  "raw_uri": "https://example.com/longlongstuff",
  "encoded_uri": "https://example.com/longlongstuff"
}
```

> 400 Bad Request:

```json
{ "msg": "Invalid URI." }
```

Create a shorten URI from the long URI. `id` can be used for retrieving the original URI.

### HTTP Request
`POST /shorten`

### Body
Parameter | Description
--------- | -----------
uri | The URI to be shorten.


## Retrieve Original URI

```shell
curl "https://api.abbr.ninja/api/v1/retrieve?id=aJKjknR"
```

> Response:

> 200 OK:

```json
{
  "html_safe_uri": "https://example.com/longlongstuff",
  "raw_uri": "https://example.com/longlongstuff",
  "encoded_uri": "https://example.com/longlongstuff"
}
```

> 400 Bad Request:

```json
{ "msg": "Undefined id." }
```

> 404 Not Found:

```json
{ "msg": "ID not found." }
```

This endpoint retrieves the original URI associated with a valid ID.

### HTTP Request

`GET /retrieve?id=<ID>`

### Query String Parameters

Parameter | Description
--------- | -----------
ID | The ID returned when the original URI is shorten.

# Server Status

## Query Current Server Status

```shell
curl "https://api.abbr.ninja/api/v1/status"
```

> Response:

> 200 OK:

```json
{ "status": "Ok" }
```

Query server status. `status` can be either `Ok`, `Maintenance` or `Down`.

### HTTP Request

`GET /status`
