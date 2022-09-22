# @authOrApiAuth

The `@authOrApiAuth` directive indicates that an endpoint can be accessed by an authenticated user with the same flow as the `[@auth](@auth%20f655ca4b089d4e438de5d3874d8ee2c0.md)` directive _or_ by passing in a Truffle API key as the Authorization header.

```graphql
Authorization: `Bearer ${apiKey}`
```

```jsx
curl --location --request POST 'https://mycelium.staging.bio/graphql' \
--header 'Authorization: Bearer sk_6ayv42OwaLZt8n9Ej46F35ldDw6h8ZuXxeoC79hypu9LVCWMHIoRP6CWq0XmxImnnbOYpyLtlAayMshHqfL0jMGEWlmXZoENwXUEADxSFRt7L' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"query UserById ($input: UserInput) {\n    user(input: $input) {\n      id\n      name\n      time\n    }\n}","variables":{"input":{"id":"<userId>"}}}'
```
