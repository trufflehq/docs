---
description: A season pass (Battle Pass) that has levels and associated rewards
---

# SeasonPass

### Resolvers

`seasonPass`

Returns a season pass (battle pass)

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a season pass
"""
seasonPass(input: SeasonPassInput): SeasonPass @authOrApiAuth
```

**Input**

`SeasonPassInput`

| Argument | Type | Description           |
| -------- | ---- | --------------------- |
| id       | ID   | ID of the season pass |

**Query**

```graphql
query SeasonPassQuery ($input: SeasonPassInput!) {
    seasonPass(input: $input) {
      id
      orgId
      name
      data
      levels {
        levelNum
        minXp
        rewards {
            tierNum
            sourceType
            sourceId
            description
            amountValue
        }
      }  
      orgUserCounterTypeId
      startTime
      endTime
      daysRemaining
    }
}
```

**Variables**

```graphql
{
  "input": {
     "id": "b0de9fc0-41c7-11ec-b5b0-5067f646709b"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "seasonPass": {
      "id": "d1d12450-8538-11ec-9e07-5bda097f4285",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "name": "Shroom Pass",
      "data": {
        "tiers": [
          { "name": "Merch", "background": "#EB321A" },
          {
            "name": "Crypto-eligible",
            "background": "linear-gradient(91.66deg, #EB321A 0.42%, #A4419F 49.09%, #1D40D7 103.82%)"
          }
        ]
      },
      "levels": [
        {
          "levelNum": 1,
          "minXp": 1,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": 10
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": 10
            }
          ]
        },
        {
          "levelNum": 2,
          "minXp": 3,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": null
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": null
            }
          ]
        },
        {
          "levelNum": 3,
          "minXp": 5,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": null
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": null
            }
          ]
        },
        {
          "levelNum": 4,
          "minXp": 7,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": null
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": null
            }
          ]
        },
        {
          "levelNum": 5,
          "minXp": 9,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": 10
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": 10
            }
          ]
        },
        {
          "levelNum": 6,
          "minXp": 11,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": null
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": null
            }
          ]
        },
        {
          "levelNum": 7,
          "minXp": 13,
          "rewards": [
            {
              "tierNum": 0,
              "sourceType": "collectible",
              "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
              "description": "Merch giveaway entry",
              "amountValue": null
            },
            {
              "tierNum": 1,
              "sourceType": "collectible",
              "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
              "description": "Crypto giveaway entry",
              "amountValue": null
            }
          ]
        }
      ],
      "orgUserCounterTypeId": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
      "startTime": "2022-02-07T23:32:42.658Z",
      "endTime": "2024-11-25T09:00:00.000Z",
      "daysRemaining": 892
    }
  },
  "extensions": { "components": {} }
}
```

***

`seasonPassConnection`

Returns a paginated list of season passes

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of season passes
"""
seasonPassConnection(first: Int, after: String, last: Int, after: String): SeasonPassConnection 
@authOrApiAuth
```

**Query**

```graphql
query SeasonPassConnectionQuery ($first: Int, $after: String, $last: Int, $before: String) {
    seasonPassConnection(first: $first, after: $after, last: $last, before: $before) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
           id
           orgId
           name
           data
           levels {
               levelNum
               minXp
               rewards {
                   tierNum
                   sourceType
                   sourceId
                   description
                   amountValue
               }
           }
           orgUserCounterTypeId
           startTime
           endTime
           daysRemaining
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
    "seasonPassConnection": {
      "totalCount": 1,
      "pageInfo": { "endCursor": null, "hasNextPage": false },
      "nodes": [
        {
          "id": "d1d12450-8538-11ec-9e07-5bda097f4285",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "name": "Shroom Pass",
          "data": {
            "tiers": [
              { "name": "Merch", "background": "#EB321A" },
              {
                "name": "Crypto-eligible",
                "background": "linear-gradient(91.66deg, #EB321A 0.42%, #A4419F 49.09%, #1D40D7 103.82%)"
              }
            ]
          },
          "levels": [
            {
              "levelNum": 1,
              "minXp": 1,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": 10
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": 10
                }
              ]
            },
            {
              "levelNum": 2,
              "minXp": 3,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": null
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": null
                }
              ]
            },
            {
              "levelNum": 3,
              "minXp": 5,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": null
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": null
                }
              ]
            },
            {
              "levelNum": 4,
              "minXp": 7,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": null
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": null
                }
              ]
            },
            {
              "levelNum": 5,
              "minXp": 9,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": 10
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": 10
                }
              ]
            },
            {
              "levelNum": 6,
              "minXp": 11,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": null
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": null
                }
              ]
            },
            {
              "levelNum": 7,
              "minXp": 13,
              "rewards": [
                {
                  "tierNum": 0,
                  "sourceType": "collectible",
                  "sourceId": "10419110-d7ce-11ec-b415-51e0f899cca7",
                  "description": "Merch giveaway entry",
                  "amountValue": null
                },
                {
                  "tierNum": 1,
                  "sourceType": "collectible",
                  "sourceId": "849ed7c0-d7ce-11ec-937a-13eebb512ac4",
                  "description": "Crypto giveaway entry",
                  "amountValue": null
                }
              ]
            }
          ],
          "orgUserCounterTypeId": "c7831ba0-41bf-11ec-80cc-e9cdb03a1057",
          "startTime": "2022-02-07T23:32:42.658Z",
          "endTime": "2024-11-25T09:00:00.000Z",
          "daysRemaining": 892
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`OrgUser.seasonPass`

Resolves a season pass for an org user. This is usually used to get an org user’s progress for a given season pass.

OrgUser

***

`Connection.seasonPass`

Resolves a season pass for a connection. This is usually used to resolve season pass progress based on a 3rd party connection e.g a youtube, twitch, minecraft, etc.

Connection

***

`YoutubeChannel.seasonPass`

Resolves a season pass for a YouTube channel. This is used to fetch the season pass to render inside of the YouTube emoji picker

***

***

### Mutations

`seasonPassUpsert`

Create/update a season pass

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a seasonPass

```graphql
"""
Create/update a season pass
"""
seasonPassUpsert(
  input: SeasonPassUpsertInput
): SeasonPassUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { seasonPass: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`SeasonPassUpsertInput`

| Argument  | Type   | Description                                     |
| --------- | ------ | ----------------------------------------------- |
| id        | ID     | ID of the season pass                           |
| name      | String | Name of the season pass                         |
| startTime | Date   | Start time of the season pass                   |
| endTime   | Date   | When the season pass is over                    |
| levels    | JSON   | List of levels for the season pass              |
| data      | JSON   | Additional data associated with the season pass |

**Query**

```graphql
mutation SeasonPassUpsert ($input: SeasonPassUpsertInput!) {
    seasonPassUpsert(input: $input) {
        seasonPass {
            id
            name
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "name": "June Season Pass",
      "startTime": "2022-06-01T06:00:00.000Z", // iso format
      "endTime": "2022-07-01T06:00:00.000Z", // iso format
      "levels": [
          {
            "levelNum":1,"minXp":5,
            "rewards":[
                {
                    "sourceType":"collectible",
                    "sourceId":"8b4727c0-393c-11ec-9b1e-2b235c64484e",
                    "tierNum":0,
                    "description":"Unlock the StanzYOU emote"
                }
            ]
          }
      ]
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "seasonPassUpsert": {
      "seasonPass": {
        "id": "6490df50-edcc-11ec-a34c-5b7f817b6da4",
        "name": "June Season Pass"
      }
    }
  },
  "extensions": { "components": {} }
}
```

***
