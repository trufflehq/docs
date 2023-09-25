---
description: >-
  An action used to update state associated with battle passes, collectibles,
  predictions, etc.
---

# EconomyAction

### Resolvers

`economyAction`

Returns an economy action

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns an economy action  
"""
economyAction(input: EconomyActionInput): @authOrApiAuth EconomyAction
```

**Input**

`EconomyActionInput`

| Argument         | Type | Description                                         |
| ---------------- | ---- | --------------------------------------------------- |
| id               | ID   | ID of the economy action                            |
| economyTriggerId | ID   | The ID of the economy trigger that fires the action |

Right now there is a list of default economy triggers that are built in to truffle that you can use to trigger an economy action through the platform. Here is a page with all of the available triggers with their IDs.

**Query**

```graphql
query EconomyActionQuery ($input: EconomyActionInput!) {
    economyAction(input: $input) {
      id
      orgId
      name
      amountType
      amountId
      amountValue
      amountSourceType
      isVariableAmount
      economyTriggerId
      data {
          description
          timeScale
          numActions
          maxActions
          cooldownSeconds
          actionLink
          amountDescription
          redeemData
      }
    }
}
```

**Variables**

```graphql
{
  "input": {
     "economyTriggerId": "3a2de150-6f68-11ec-b706-956d4fcf75c0"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "economyAction": {
      "id": "8e707440-8538-11ec-a3ff-5ff20225f34b",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "name": "Forum Create Post",
      "amountType": "orgUserCounterType",
      "amountId": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
      "amountValue": 1,
      "amountSourceType": null,
      "isVariableAmount": false,
      "economyTriggerId": "3a2de150-6f68-11ec-b706-956d4fcf75c0",
      "data": {
        "description": "Create a post in the forum",
        "timeScale": "day",
        "numActions": null,
        "maxActions": 500,
        "cooldownSeconds": null,
        "actionLink": null,
        "amountDescription": null,
        "redeemData": { "seasonPassId": "d1d12450-8538-11ec-9e07-5bda097f4285" }
      }
    }
  },
  "extensions": { "components": {} }
}
```



`economyActionConnection`

Returns a paginated list of economy actions

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of EconomyActions.
"""
economyActionConnection(
	input: EconomyActionConnectionInput,
	first: Int,
	after: String,
	last: Int,
	before: String
): EconomyActionConnection 
@authOrApiAuth
```

**Input**

`EconomyActionConnectionInput`

| Argument   | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| amountType | String | Type of amount the economy action is for |

Leave blank to return all of the economy actions for an org

**Query**

```graphql
query EconomyActionConnectionQuery ($input: EconomyActionConnectionInput, $first: Int, $after: String, $last: Int, $before: String) {
    economyActionConnection(input: $input, first: $first, after: $after, last: $last, before: $before) {
        pageInfo {
            endCursor
            hasNextPage
            startCursor
            hasPreviousPage
        }
        nodes {
            id
            orgId
            name
            amountType
            amountId
            amountValue
            amountSourceType
            isVariableAmount
            economyTriggerId
            data {
                description
                timeScale
                numActions
                maxActions
                cooldownSeconds
                actionLink
                amountDescription
                redeemData
            }
        }
    }
}
```

**Variables**

```graphql
{
    "first": 2,
		"after": "ZtlWQJ",
    "input": {
        "amountType": "orgUserCounterType"
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "economyActionConnection": {
      "totalCount": 2,
      "pageInfo": {
        "endCursor": "M5xva",
        "hasNextPage": true,
        "startCursor": "ZtlWQJ",
        "hasPreviousPage": true
      },
      "nodes": [
        {
          "id": "c70b4550-ae64-11ec-9571-dd01980fb9d3",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "name": "Twitter User Retweet",
          "amountType": "orgUserCounterType",
          "amountId": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
          "amountValue": 1,
          "amountSourceType": null,
          "isVariableAmount": false,
          "economyTriggerId": "1a146970-6f68-11ec-b706-956d4fcf75c0",
          "data": {
            "description": "Retweet Stanz's tweets",
            "timeScale": "day",
            "numActions": null,
            "maxActions": 3,
            "cooldownSeconds": null,
            "actionLink": null,
            "amountDescription": null,
            "redeemData": {
              "seasonPassId": "d1d12450-8538-11ec-9e07-5bda097f4285"
            }
          }
        },
        {
          "id": "2f12caf0-9f7a-11ec-ac07-5329e41611c5",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "name": "Win a prediction",
          "amountType": "orgUserCounterType",
          "amountId": "cde02510-9741-11ec-b978-0dc2009053ba",
          "amountValue": 0,
          "amountSourceType": null,
          "isVariableAmount": true,
          "economyTriggerId": "5807bc10-80c4-11ec-a5c9-01fed7cc1cdc",
          "data": {
            "description": "When Ludwig creates a prediction, you have the option to place a bet between 2 outcomes. Place a bet on one of the options with an amount of your channel points. If you bet on the winning outcome, you get a proportional amount of the channel points pool.",
            "timeScale": null,
            "numActions": null,
            "maxActions": null,
            "cooldownSeconds": null,
            "actionLink": null,
            "amountDescription": "Proportional amount of the pool",
            "redeemData": null
          }
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```



`SeasonPass.economyActionConnection`

Resolves a paginated list of economy actions for a season pass. This is usually used to fetch all of the economy actions associated with a season pass.

**Input**

| Argument | Type   | Description                        |
| -------- | ------ | ---------------------------------- |
| first    | Int    | Page size for forwards pagination  |
| after    | String | forward pagination cursor          |
| last     | Int    | Page size for backwards pagination |
| before   | String | backwards pagination cursor        |

SeasonPass



`EconomyTransaction.economyAction`

Resolves an economy action from an economy transaction. This is usually used to fetch information about the action that created the economy action.

EconomyTransaction





### Mutations

`economyActionUpsert`

Creates/updates an economy action

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ an economy action

```graphql
"""
Creates/updates an economy action
"""
economyActionUpsert(
  input: EconomyActionUpsertInput
): EconomyActionUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { economyAction: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`EconomyActionUpsertInput`

| Argument         | Type    | Description                                                                               |
| ---------------- | ------- | ----------------------------------------------------------------------------------------- |
| id               | ID      | ID of an EconomyAction                                                                    |
| name             | String  | Name of the EconomyAction                                                                 |
| economyTriggerId | ID      | ID of the trigger for the economy action                                                  |
| amountType       | String  | Type of amount the economy action modifies                                                |
| amountId         | String  | ID of the amountType                                                                      |
| amountValue      | Float   | Value of the specified amount                                                             |
| isVariableAmount | Boolean | Whether the EconomyAction modification is for a static or variable amount e.g predictions |
| data             | JSON    | Additional data associated with an economy action                                         |

**Query**

For example if you wanted to increase the max number of times a user could reply to a creator (Stanz) in one day, you could use the following query and update the `maxActions` attribute in the `data` argument

```graphql
mutation EconomyActionUpsert ($input: EconomyActionUpsertInput!) {
    economyActionUpsert(input: $input) {
       economyAction {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "ca1b9290-ae64-11ec-9571-dd01980fb9d3",
      "data": {
          "description":"Reply to Stanz's tweets","redeemType":"seasonPassParticipate","timeScale":"day","maxActions":5,"redeemData":{
              "seasonPassId":"d1d12450-8538-11ec-9e07-5bda097f4285"
            }
        }
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "economyActionUpsert": {
      "economyAction": { "id": "ca1b9290-ae64-11ec-9571-dd01980fb9d3" }
    }
  },
  "extensions": { "components": {} }
}
```

