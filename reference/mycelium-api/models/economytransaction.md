---
description: >-
  Returns a transaction started by an economy action. This model is used as a
  ledger to keep track of all of the actions that have happened to a user.
---

# EconomyTransaction

### Resolvers

`economyTransactionConnection`

Returns a list of economy transactions

**Note: Pagination is not currently supported for this resolver. You can still pass in `first` to specify the result size though**

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of EconomyTransactions
"""
economyTransactionConnection(input: EconomyActionConnectionInput, first: Int, after: String, last: Int, before: String): EconomyTransactionConnection 
@authOrApiAuth
```

**Input**

`EconomyTransactionConnectionInput`

| Argument   | Type   | Description                                     |
| ---------- | ------ | ----------------------------------------------- |
| userId     | ID     | The userId for an EconomyTransaction            |
| amountType | String | The type of amount for the EconomyTransaction   |
| amountId   | ID     | The id of the amount for the EconomyTransaction |

`first`

| Argument | Type | Description                             |
| -------- | ---- | --------------------------------------- |
| first    | Int  | Specify the number of results to return |

**Query**

```graphql
query EconomyTransactionConnectionQuery ($input: EconomyTransactionConnectionInput, $first: Int) {
    economyTransactionConnection(input: $input, first: $first) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
            startCursor
            hasPreviousPage
        }
        nodes {
           id
           amountId
           amountType
           amountValue
           userId
           date
        }
    }
}
```

**Variables**

```graphql
{
    "first": 3,
    "input": {
        "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
        "amountType": "orgUserCounterType",
        "amountId": "cde02510-9741-11ec-b978-0dc2009053ba"
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "economyTransactionConnection": {
      "totalCount": 3,
      "pageInfo": null,
      "nodes": [
        {
          "id": "51413590-a93d-11ec-935e-9592005929c7",
          "amountId": "cde02510-9741-11ec-b978-0dc2009053ba",
          "amountType": "orgUserCounterType",
          "amountValue": 50,
          "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
          "date": "2022-03-21T17:35:36.297Z"
        },
        {
          "id": "3964a880-a93d-11ec-839a-23b9c513cf01",
          "amountId": "cde02510-9741-11ec-b978-0dc2009053ba",
          "amountType": "orgUserCounterType",
          "amountValue": 25,
          "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
          "date": "2022-03-21T17:34:56.264Z"
        },
        {
          "id": "154fc010-a93d-11ec-a190-a0036a89514a",
          "amountId": "cde02510-9741-11ec-b978-0dc2009053ba",
          "amountType": "orgUserCounterType",
          "amountValue": 25,
          "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
          "date": "2022-03-21T17:33:55.729Z"
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`OrgUserCounter.economyTransactionConnection`

Returns a paginated list of economy transactions. This is typically used to fetch a user’s transaction history for a specific org user counter. e.g fetching all channel point or xp transactions.

OrgUserCounter

***

`Donation.economyTransaction`

Returns a specific economy transaction for a donation.

***

***

### Mutations

`economyTransactionCreate`

Create an economy transaction

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permissions**

must have permission to _update_ an economyTransaction

```graphql
"""
Creates an economy transaction
"""
economyTransactionCreate(input: EconomyTranscationCreateInput): EconomyTranscationCreatePayload 
@authOrApiAuth     
@hasPermissions(
    filters: { economyTransaction: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`EconomyTranscationCreateInput`

| Argument           | Type   | Description                                             |
| ------------------ | ------ | ------------------------------------------------------- |
| economyTriggerId   | ID     | The ID of the trigger                                   |
| economyActionId    | ID     | ID of the economy action                                |
| orgId              | ID     | ID of the org                                           |
| userId             | ID     | ID of the user                                          |
| additionalData     | JSON   | Additional data associated with the economy transaction |
| amountSourceId     | String | 3rd party amount ID                                     |
| amountValue        | Float  | 3rd party amount                                        |
| economyTriggerSlug | String | Slug that triggers the transaction                      |

**Query**

If someone purchased a higher tier of the battle pass through your application, you could issue the following request

```graphql
mutation EconomyTransactionCreate ($input: EconomyTranscationCreateInput!) {
    economyTransactionCreate(input: $input) {
       economyTransaction {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "economyTriggerSlug": "tier-unlock",
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7"

  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "economyTransactionCreate": {
      "economyTransaction": { "id": "e37e2cc0-edc5-11ec-81c3-1d021bcc4c33" }
    }
  },
  "extensions": { "components": {} }
}
```

***
