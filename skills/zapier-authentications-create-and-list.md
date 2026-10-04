---
name: zapier-authentications-create-and-list
description: Retrieve existing authentications and then create a new authentication.
api: openapi/zapier-authentications-api-openapi.yml
operations:
- get-authentications
- create-authentication
generated: '2026-10-04'
method: generated
generator: extract-docs-artifacts.py skills (local)
source: openapi/zapier-authentications-api-openapi.yml ; every operationId checked against the contract
---

# zapier-authentications-create-and-list

Retrieve existing authentications and then create a new authentication.

## Steps

1. 1. Call `get-authentications` – no query parameters or request body are documented.
2. 2. Call `create-authentication` – no request body fields or headers are documented.

## Rules

- Authentication: use either ClientIDAuthentication (apiKey) or OAuth (oauth2) as described in the auth schemes.
- Rate limiting: no rate limit is defined; on exhaustion the API returns no specific HTTP status.
