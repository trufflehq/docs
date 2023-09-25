---
description: A user's progression through a season pass
---

# SeasonPassProgression

### Resolvers

`SeasonPass.seasonPassProgression`

Resolves a user’s SeasonPassProgression for a specific SeasonPass. This is typically used to get a user’s current level in the season pass.

**Input**

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| userId   | ID   | ID of the user |

SeasonPass



### Mutations

`seasonPassProgressionUpsert`

Update an existing season pass progression. Creates aren’t currently supported yet. If you need this for your use case please contact us.

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a SeasonPassProgression

```graphql
seasonPassProgressionUpsert(input: SeasonPassProgressionUpsertInput): SeasonPassProgressionUpsertPayload 
@authOrApiAuth 
@hasPermissions(filters: { seasonPassProgression: { idArg: "id", rank: 0 } }, action: "update")
```

**Input**

`SeasonPassProgressionUpsertInput`

| Argument     | Type | Description                                                                                                                               |
| ------------ | ---- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| id           | ID   | ID of the existing season pass progression                                                                                                |
| tierNum      | Int  | Tier number of the season pass. This is used to modify the season pass progress tier e.g a user purchases access to a premium battle pass |
| userId       | ID   | ID of the user                                                                                                                            |
| seasonPassId | ID   | ID of the season pass the user is progressing through                                                                                     |

**Query**

```graphql
mutation SeasonPassProgressionUpsert ($input: SeasonPassProgressionUpsertInput!) {
    seasonPassProgressionUpsert(input: $input) {
        seasonPassProgression {
            id
            tierNum
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
     "id": "715c9b80-a938-11ec-ac72-384f816c404e",
     "tierNum": 1
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "seasonPassProgressionUpsert": {
      "seasonPassProgression": {
        "id": "715c9b80-a938-11ec-ac72-384f816c404e",
        "tierNum": 1
      }
    }
  },
  "extensions": { "components": {} }
}
```

