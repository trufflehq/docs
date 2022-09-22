# @auth

The `@auth` directive indicates that a given field requires that the request originates from an authenticated user and cannot be accessed directly via an API key. Most endpoints restricted with this directive refer directly to user settings.

The request for fields restricted by this directive must pass a Truffle user access token with the request as a `x-access-token` header and specify ID of the org you’re performing the request against with the `x-org-id` header.

**Example**

```jsx
curl --location --request POST 'https://mycelium.staging.bio/graphql' \
--header 'x-access-token: <accessToken>' \
--header 'x-org-id: <orgId>' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"query UserGetMe {\n    me {\n      id\n      name\n      email\n      time\n      country\n      hasStripeId\n      hasPassword\n    }\n}","variables":{}}'
```
