---
description: >-
  A counter for User on an Org. These are commonly used for things like XP in
  the battle pass, channel points, or any other type of counter.
---

# OrgUserCounter

### Resolvers

`orgUserCounter`

Returns an org user counter

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns an org user counter
"""
orgUserCounter(
  input: OrgUserCounterInput
): OrgUserCounter 
@authOrApiAuth
```

**Input**

`OrgUserCounterInput`

| Argument             | Type | Description                         |
| -------------------- | ---- | ----------------------------------- |
| userId               | ID   | The ID of the user                  |
| orgId                | ID   | The ID of the org                   |
| orgUserCounterTypeId | ID   | The ID of the org user counter type |

**Query**

```graphql
query OrgUserCounterQuery ($input: OrgUserCounterInput!) {
    orgUserCounter(input: $input) {
      userId
      orgId
      orgUserCounterTypeId
      count
    }
}
```

**Variables**

```graphql
{
  "input": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "orgUserCounterTypeId": "cde02510-9741-11ec-b978-0dc2009053ba"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserCounter": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "orgUserCounterTypeId": "cde02510-9741-11ec-b978-0dc2009053ba",
      "count": "1200"
    }
  },
  "extensions": { "components": {} }
}
```

***

`orgUserCounterConnection`

Returns a list of org user counters. This is usually used to return a leaderboard.

**Note: pagination is not currently supported on this endpoint. You can pass in `first` to specify the page size returned**

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of org user counters

NOTE: Pagination is under 🚧
"""
orgUserCounterConnection(
  input: OrgUserCounterConnectionInput
  first: Int
  after: String
  last: Int
  before: String
): OrgUserCounterConnection @authOrApiAuth
```

**Input**

`OrgUserCounterConnectionInput`

| Argument             | Type | Description                         |
| -------------------- | ---- | ----------------------------------- |
| orgUserCounterTypeId | ID   | The ID of the org user counter type |

`first`

| Argument | Type | Description                                                |
| -------- | ---- | ---------------------------------------------------------- |
| first    | Int  | A limit on the size of the results returned. Default is 25 |

**Query**

```graphql
query OrgUserCounterConnectionQuery ($input: OrgUserCounterConnectionInput, $first: Int) {
    orgUserCounterConnection(input: $input, first: $first) {
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
          userId
          count
        }
    }
}
```

**Variables**

```graphql
{
    "input": {
        "orgUserCounterTypeId": "cde02510-9741-11ec-b978-0dc2009053ba"
    }
}
```

**Sample Response**

```graphql
{
  "data": { "orgUserCounterConnection": { "pageInfo": null, "nodes": [
    {
      "userId": "f3543ec0-edb9-11ec-b882-c1adca2b5ac7",
      "count": 200
    },
    {
      "userId": "fb3d1620-edb9-11ec-b882-c1adca2b5ac7",
      "count": 50
    }
  ] } },
  "extensions": { "components": {} }
}
```

***

`SeasonPass.orgUserCounter`

Resolves a user's progress in a season pass (XP).

`userId`

| Argument | Type | Description                      |
| -------- | ---- | -------------------------------- |
| userId   | ID   | ID of the user to resolve XP for |

SeasonPass

***

`SeasonPass.orgUserStats`

Resolves a set of season pass stats for the user

`userId`

| Argument | Type | Description                                     |
| -------- | ---- | ----------------------------------------------- |
| userId   | ID   | ID of the user to resolve season pass stats for |

***

***

### Mutations

`orgUserCounterIncrement`

Increment an org user counter

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

Must have permission to _update_ an org user counter

```graphql
"""
Increment an org user counter
"""
orgUserCounterIncrement(
  input: OrgUserCounterIncrementInput
): OrgUserCounterIncrementPayload 
@authOrApiAuth
@hasPermissions(
  filters: { orgUserCounter: { idArg: "id", rank: 0 } }
  action: "update"
)
```

**Input**

`OrgUserCounterIncrementInput`

| Argument             | Type | Description                      |
| -------------------- | ---- | -------------------------------- |
| userId               | ID   | ID of the user                   |
| orgUserCounterTypeId | ID   | ID of the org user counter type  |
| count                | Int  | Amount to increment/decrement by |

**Query**

```graphql
mutation OrgUserCounterIncrementQuery ($input: OrgUserCounterIncrementInput) {
    orgUserCounterIncrement(input: $input) {
       isUpdated
    }
}
```

**Variables**

```graphql
{
  "input": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "orgUserCounterTypeId": "cde02510-9741-11ec-b978-0dc2009053ba",
      "count": 20
  }
}
```

**Sample Response**

```graphql
{
  "data": { "orgUserCounterIncrement": { "isUpdated": true } },
  "extensions": { "components": {} }
}
```

***

### Mutations

`orgUserCounterUpsert`

Replaces an org user counter

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

Must have permission to _update_ an org user counter

```graphql
"""
Updates an org user counter (replaces the amount instead of incrementing/decrementing)
"""
orgUserCounterUpsert(
  input: OrgUserCounterUpsertInput
): OrgUserCounterUpsertPayload
@authOrApiAuth 
@hasPermissions(
  filters: { orgUserCounter: { idArg: "id", rank: 0 } }
  action: "update"
)
```

**Input**

`OrgUserCounterIncrementInput`

| Argument             | Type | Description                      |
| -------------------- | ---- | -------------------------------- |
| userId               | ID   | ID of the user                   |
| orgUserCounterTypeId | ID   | ID of the org user counter type  |
| count                | Int  | Amount to increment/decrement by |

**Query**

```graphql
mutation OrgUserCounterUpsertQuery ($input: OrgUserCounterUpsertInput) {
    orgUserCounterUpsert(input: $input) {
       isUpdated
    }
}
```

**Variables**

```graphql
{
  "input": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "orgUserCounterTypeId": "cde02510-9741-11ec-b978-0dc2009053ba",
      "count": 20
  }
}
```

**Sample Response**

```graphql
{
  "data": { "orgUserCounterUpsert": { "isUpdated": true } },
  "extensions": { "components": {} }
}
```
