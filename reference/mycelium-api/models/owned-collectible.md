---
description: Collectibles that a user owns
---

# Owned Collectible

### Resolvers

`ownedCollectibleConnection`

Returns a paginated list of OwnedCollectibles

**Directives:**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` : requires access token or valid api key

```graphql
"""
  Returns a paginated list of OwnedCollectibles
  """
  ownedCollectibleConnection(
    input: OwnedCollectibleConnectionInput
    first: Int
    after: String
    last: Int
    before: String
  ): OwnedCollectibleConnection @authOrApiAuth
```

**Input**

`OwnedCollectibleConnectionInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| orgId    | ID   | ID of the org  |
| userId   | ID   | ID of the user |

**Query**

```graphql
query OwnedCollectibleConnection ($input: OwnedCollectibleConnectionInput) {
    ownedCollectibleConnection(input: $input) {
        totalCount
        pageInfo {
            startCursor
            hasPreviousPage
            endCursor
            hasNextPage
        }
        nodes {
            userId
            collectibleId
            count
        }
    }
}
```

**Variables**

```graphql
{
   "input": {
       "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
       "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7"
   }
}
```

**Sample Response**

```graphql
{
  "data":
    {
      "ownedCollectibleConnection":
        {
          "totalCount": 3,
          "pageInfo":
            {
              "startCursor": null,
              "hasPreviousPage": false,
              "endCursor": null,
              "hasNextPage": false,
            },
          "nodes":
            [
              {
                "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
                "collectibleId": "64c7f610-393c-11ec-9b1e-2b235c64484e",
                "count": 1,
              },
              {
                "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
                "collectibleId": "7723d220-393c-11ec-9b1e-2b235c64484e",
                "count": 1,
              },
              {
                "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
                "collectibleId": "80bb9200-393c-11ec-9b1e-2b235c64484e",
                "count": 1,
              }
            ],
        },
    },
  "extensions": { "components": {} },
}
```

***

`Collectible.ownedCollectible`

Resolves an owned collectible from a collectible. This is typically used if you want to query for a set of collectibles (e.g an org’s collectibles) and resolve the counts that a user owns for each collectible.

Collectible

***

`OrgUser.ownedCollectibleConnection`

Resolves a list of all of the owned collectibles for an org user. This is typically used to pull all of the collectibles for a requested org user.

**Input**

`OwnedCollectibleConnectionInput`

| Argument        | Type   | Description                                         |
| --------------- | ------ | --------------------------------------------------- |
| collectibleType | String | The type of collectible e.g emote, redeemable, etc. |

OrgUser

***

### Mutations

`ownedCollectibleRedeem`

Redeems an owned collectible. This is typically used when a user would like to redeem one of their collectibles. e.g activating flair, redeeming a custom discord role, redeeming a 3rd party action.

**Directives:**

`@authOrApiAuth`: requires access token or valid api key

**Permission**

User must have access to update ownedCollectible, user can update their own ownedCollectible

```graphql
"""
Redeem an owned collectible
"""
ownedCollectibleRedeem(input: OwnedCollectibleRedeemInput): OwnedCollectibleRedeemPayload 
@auth
@hasPermissions(filters: { ownedCollectible: { idArg: "id", rank: 0 } }, action: "update")
```

**Query**

```graphql
mutation OwnedCollectibleRedeem ($input: OwnedCollectibleRedeemInput) {
    ownedCollectibleRedeem(input: $input) {
        redeemResponse
        redeemError
    }
	}
```

**Variables**

```graphql
{
   "input": {
       "collectibleId": "ebb62860-6cca-11ec-ad84-15c1691b5c6b",
			 "additionalData": {}
   }
}
```

**Sample Response**

Redeems a collectible pack

```graphql
{
  "data": {
    "ownedCollectibleRedeem": {
      "redeemResponse": {
        "type": "collectiblePack",
        "collectibleIds": ["7a909740-393c-11ec-9b1e-2b235c64484e"]
      },
      "redeemError": null
    }
  },
  "extensions": { "components": {} }
}
```

***

`ownedCollectibleIncrement`

Increment a user’s owned collectibles. This is typically called when a user earns or buys a reward, this mutation handles the increase/decrease of the user’s collectible inventory.

Want to make sure that this is restricted to only admin so users can’t increment their own owned collectibles

**Directives:**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

**Permission:**

requires permission to _update_ ownedCollectibles

**Query**

```graphql
mutation OwnedCollectibleIncrement ($input: OwnedCollectibleIncrementInput) {
    ownedCollectibleIncrement(input: $input) {
        collectible { 
            id
        }
        count
    }
}
```

**Variables**

```graphql
{
   "input": {
       "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
       "collectibleId": "ebb62860-6cca-11ec-ad84-15c1691b5c6b",
       "count": 3
   }
}
```

**Sample Response**

```graphql
{
  "data": {
    "ownedCollectibleIncrement": {
      "collectible": { "id": "ebb62860-6cca-11ec-ad84-15c1691b5c6b" },
      "count": 3
    }
  },
  "extensions": { "components": {} }
}
```
