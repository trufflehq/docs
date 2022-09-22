---
description: A powerup that the user has activated
---

# Active Powerup

### Resolvers

`activePowerupConnection`

Returns a paginated list of active powerups

**Directives**

`@authOrApiAuth`

```graphql
"""
Get a paginated list of an authenticated user's active powerups
"""
activePowerupConnection(
  first: Int
  after: String
  last: Int
  before: String
): ActivePowerupConnection @auth
```

**Input**

`ActivePowerupConnectionInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| userId   | ID   | ID of the user |

**Query**

```graphql
query ActivePowerupConnectionQuery ($first: Int, $after: String, $last: Int, $before: String) {
    activePowerupConnection(first: $first, after: $after, last: $last, before: $before) {
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
            id
            userId
            orgId
            slug
            name
            type
            data {
                rgba
                value
            }
            creationDate
        }
    }
}
```

**Variables**

```graphql
{
  "first": 5
}
```

**Sample Response**

```graphql
{
  "data": {
    "activePowerupConnection": {
      "pageInfo": { "endCursor": null, "hasNextPage": false },
      "nodes": [
        {
          "id": "1599cf20-ed9e-11ec-8bbb-aeeeb763ec8c",
          "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "powerupId": "def483b0-857f-11ec-a3ff-5ff20225f34b",
          "sourceType": "user",
          "sourceId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
          "data": { "rgba": null, "value": null },
          "creationDate": "2022-06-16T17:59:36.466Z"
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`Article.activePowerupConnection`

resolves a list of active powerups applied to an article.

***

`OrgUser.activePowerupConnection`

resolves a list of active powerups activated by an org user. This is usually used to get another user’s active powerups e.g flair, name gradient, chat highlight message, etc.

OrgUser

***

### Mutations

`activePowerupDeleteById`

Deletes an active powerup

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can delete with authenticated user

**Permissions**

Must have permission to delete an active powerup

**Input**

`ActivePowerupDeleteByIdInput`

| Argument | Type | Description              |
| -------- | ---- | ------------------------ |
| id       | ID   | ID of the active powerup |
| userId   | ID   | ID of the user           |

**Query**

```graphql
mutation ActivePowerupDeleteById ($input: ActivePowerupDeleteByIdInput!) {
    activePowerupDeleteById(input: $input) {
       activePowerup {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "1599cf20-ed9e-11ec-8bbb-aeeeb763ec8c"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "activePowerupDeleteById": {
      "activePowerup": { "id": "1599cf20-ed9e-11ec-8bbb-aeeeb763ec8c" }
    }
  },
  "extensions": { "components": {} }
}
```
