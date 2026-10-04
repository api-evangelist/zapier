---
name: zapier-get-input-fields-and-choices
description: Retrieve the input fields for an action and then fetch the available choices for a specific input.
api: openapi/zapier-inputs-api-openapi.yml
operations:
- get-fields-inputs
- get-choices
generated: '2026-10-04'
method: generated
generator: extract-docs-artifacts.py skills (local)
source: openapi/zapier-inputs-api-openapi.yml ; every operationId checked against the contract
---

# zapier-get-input-fields-and-choices

Retrieve the input fields for an action and then fetch the available choices for a specific input.

## Steps

1. 1. Call `get-fields-inputs` with the required path parameter `action_id` and any request body fields defined by the contract.
2. 2. Call `get-choices` with the required path parameters `action_id` and `input_id` and any request body fields defined by the contract.

## Rules

- Authentication: Provide either a `ClientIDAuthentication` API key in the `Authorization` header or an OAuth2 bearer token.
- Idempotency: Not applicable; the operations are not idempotent.
- Pagination: Not applicable; the responses are not paginated.
- Errors: The API returns standard HTTP error codes; no specific error handling is documented.
