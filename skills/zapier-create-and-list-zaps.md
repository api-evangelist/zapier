---
name: zapier-create-and-list-zaps
description: Create a new Zap and then retrieve the list of Zaps.
api: openapi/zapier-zaps-api-openapi.yml
operations:
- post-zaps
- get-v2-zaps
generated: '2026-10-04'
method: generated
generator: extract-docs-artifacts.py skills (local)
source: openapi/zapier-zaps-api-openapi.yml ; every operationId checked against the contract
---

# zapier-create-and-list-zaps

Create a new Zap and then retrieve the list of Zaps.

## Steps

1. 1. Use `post-zaps` with the request body fields required to define the Zap.
2. 2. Use `get-v2-zaps` to retrieve the updated list of Zaps.

## Rules

- Authentication: include either a `Client-ID` header for API key authentication or an `Authorization: Bearer <token>` header for OAuth2.
- Pagination: `get-v2-zaps` supports standard pagination via `page` and `page_size` query parameters.
