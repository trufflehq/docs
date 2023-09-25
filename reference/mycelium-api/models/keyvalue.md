# KeyValue

This model is a basic Key ↔ Value mapping that can be used to store all sorts of different data. Traditionally this has been used for storing configuration data and flags but can be used for anything where you’d need a KV pair.

### Resolvers

`OrgUser.keyValueConnection`

resolves a paginated list of key values for an OrgUser.

OrgUser





### Mutations

`keyValueUpsert`

Create or update a key value

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

can only update if you have permission to _update_ key value or if you created the key value

```graphql
"""
Creates/updates a KeyValue
"""
keyValueUpsert(input: KeyValueUpsertInput!): KeyValue
  @auth
  @hasPermissions(
    filters: { keyValue: { isAll: true, rank: 0 } },
    action: "update",
    modelUserIdKey: "sourceId"
  )
```

**Input**

`KeyValueUpsertInput`

| Argument   | Type   | Description                                  |
| ---------- | ------ | -------------------------------------------- |
| sourceType | String | A type associated with the KeyValue e.g user |
| sourceId   | String | The ID associated with a sourceType          |
| key        | String | The key in the KeyValue pair                 |
| value      | String | The value in the KeyValue pair               |

**Query**

```graphql
mutation KeyValueUpsert ($input: KeyValueUpsertInput!) {
    keyValueUpsert(input: $input) {
        keyValue {
            key
            value
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "sourceType": "user",
    "sourceId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
    "key": "isMerchEligible",
    "value": "true"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "keyValueUpsert": {
      "keyValue": { "key": "isMerchEligible", "value": "true" }
    }
  },
  "extensions": { "components": {} }
}
```

