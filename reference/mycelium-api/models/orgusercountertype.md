---
description: Type of counter for users in an org
---

# OrgUserCounterType

### Resolvers

`orgUserCounterType`

Returns an OrgUserCounterType

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns an OrgUserCounterType
"""
orgUserCounterType(input: OrgUserCounterTypeInput): OrgUserCounterType @authOrApiAuth
```

**Input**

`OrgUserCounterTypeInput`

| Argument | Type   | Description                    |
| -------- | ------ | ------------------------------ |
| id       | ID     | ID of the OrgUserCounterType   |
| slug     | String | Slug of the OrgUserCounterType |

**Query**

```graphql
query OrgUserCounterTypeQuery ($input: OrgUserCounterTypeInput!) {
    orgUserCounterType(input: $input) {
      id
      slug
      name
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserCounterType": {
      "id": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
      "slug": "xp",
      "name": "XP"
    }
  },
  "extensions": { "components": {} }
}
```



`orgUserCounterTypeConnection`

Returns a paginated list of org user counter types

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of OrgUserCounterTypes
"""
orgUserCounterTypeConnection(first: Int, after: String, last: Int, before: String): OrgUserCounterTypeConnection
@authOrApiAuth
```

**Query**

```graphql
query OrgUserCounterTypeConnectionQuery ($first: Int, $after: String, $last: Int, $before: String) {
    orgUserCounterTypeConnection(first: $first, after: $after, last: $last, before: $before) {
        pageInfo {
            startCursor
            hasPreviousPage
            endCursor
            hasNextPage
        }
        nodes {
           id
           name
           slug
           decimalPlaces
        }
    }
}
```

**Variables**

```graphql
{
  "first": 3
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserCounterTypeConnection": {
      "pageInfo": {
        "startCursor": null,
        "hasPreviousPage": false,
        "endCursor": "Z2fYICB",
        "hasNextPage": true
      },
      "nodes": [
        {
          "id": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
          "name": "XP",
          "slug": "xp",
          "decimalPlaces": 0
        },
        {
          "id": "a61ab050-6c16-11ec-9ec1-582abf70e7d1",
          "name": "Extension Watch Time",
          "slug": "extension-watch-time",
          "decimalPlaces": 0
        },
        {
          "id": "d554d760-8539-11ec-a8ac-376e2c9de37a",
          "name": "Extension Watch Time Progress",
          "slug": "extension-watch-time-progress",
          "decimalPlaces": 0
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```



`EconomyTransaction.amount`

Resolves an OrgUserCounterType as the amount on an EconomyTransaction. This is typically used to return the amount for a specific economy transaction, usually used to create some sort of transaction history.

EconomyTransaction



`SeasonPass.orgUserCounterType`

Resolves an OrgUserCounterType from a season pass. This is usually used to grab the full OrgUserCounterType used to track XP in a season pass.

SeasonPass





### Mutations

`orgUserCounterTypeUpsert`

Create/update an org user counter type

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

Must have permission to _update_ an org user counter type

```graphql
"""
Create/update an org user counter type
"""
orgUserCounterTypeUpsert(
  input: OrgUserCounterTypeInput
): OrgUserCounterTypeUpsertPayload
@authOrApiAuth
@hasPermissions(
    filters: { orgUserCounterType: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`OrgUserCounterTypeUpsertInput`

| Argument      | Type   | Description                                    |
| ------------- | ------ | ---------------------------------------------- |
| id            | ID     | ID of the org user counter type                |
| name          | String | Name of the org user counter type              |
| slug          | String | Slug of the org user counter type              |
| decimalPlaces | Int    | Number of decimal places for org user counters |

**Query**

```graphql
mutation OrgUserCounterTypeUpsert ($input: OrgUserCounterTypeUpsertInput) {
    orgUserCounterTypeUpsert(input: $input) {
       orgUserCounterType {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "name": "YLYL Counter",
      "slug": "org-ylyl-count",
      "decimalPlaces": 0
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserCounterTypeUpsert": {
      "orgUserCounterType": { "id": "7f83af10-edb6-11ec-9b50-c3e235663d2c" }
    }
  },
  "extensions": { "components": {} }
}
```

