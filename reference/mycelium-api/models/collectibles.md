---
description: A digital collectible that a user can own
---

# Collectibles

#### Resolvers

`collectible`

Returns a collectible

**Directives**

`[@authOrApiAuth](<https://www.notion.so/Directives-673895108d3446118f48e9f8b881f48b>)` can read with authenticated user or valid api key

```graphql
"""
Returns a collectible
"""
collectible(input: CollectibleInput): Collectible @authOrApi
```

**Input**

`CollectibleInput`

| Argument | Type   | Description                     |
| -------- | ------ | ------------------------------- |
| id       | ID     | ID of the collectible           |
| slug     | String | Unique slug for the collectible |

**Query**

```graphql
query CollectibleQuery ($input: CollectibleInput!) {
    collectible(input: $input) {
       id
       orgId
       slug
       name
       fileRel {
           fileId
           fileObj {
               cdn
               ext
               prefix
           }
       }
       type
       targetType
       data {
           category
           redeemType
           description
           redeemData
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "64de05b0-e06a-11ec-ac50-5f44841b06b9"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "collectible": {
      "id": "64de05b0-e06a-11ec-ac50-5f44841b06b9",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "slug": "ludwig-she-her",
      "name": "She/Her Flair",
      "fileRel": {
        "fileId": null,
        "fileObj": {
          "cdn": "cdn.bio",
          "ext": "png",
          "prefix": "collectible/64de05b0-e06a-11ec-ac50-5f44841b06b9"
        }
      },
      "type": "redeemable",
      "targetType": "none",
      "data": {
        "category": "flair",
        "redeemType": "powerup",
        "description": "She/Her flair",
        "redeemData": {
          "powerupId": "a75c1df0-e06a-11ec-aa23-3cf50e9492a1",
          "durationSeconds": 2678400
        }
      }
    }
  },
  "extensions": { "components": {} }
}
```

***

`collectibleConnection`

Returns a paginated list of collectibles

**Directives**

`[@authOrApiAuth](<https://www.notion.so/Directives-673895108d3446118f48e9f8b881f48b>)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of collectibles
"""
collectibleConnection(
	input: CollectibleConnectionInput,
	first: Int,
	after: String,
	last: Int,
	before: String
): CollectibleConnection @authOrApiAuth
```

**Input**

`CollectibleConnectionInput`

| Argument   | Type   | Description                                                                                           |
| ---------- | ------ | ----------------------------------------------------------------------------------------------------- |
| type       | String | specific type of collectible e.g emote, redeemable, etc.                                              |
| orgId      | ID     | ID of the org                                                                                         |
| targetType | String | Target of the collectible, e.g if the collectible can be applied to another data type like an article |

**Query**

```graphql
query CollectibleConnectionQuery ($input: CollectibleConnectionInput, $first: Int, $after: String, $last: Int, $before: String) {
    collectibleConnection(input: $input, first: $first, after: $after, last: $last, before: $before) {
        pageInfo {
            endCursor
            hasNextPage
            startCursor
            hasPreviousPage
        }
        nodes {
            id
            orgId
            slug
            name
            fileRel {
                fileId
                fileObj {
                    cdn
                    ext
                    prefix
                }
            }
            type
            targetType
            data {
                category
                redeemType
                description
                redeemData
            }
        }
    }
}
```

**Variables**

```graphql
{
    "input": {
        "type": "emote"
    },
    "first": 3
}
```

**Sample Response**

```graphql
{
  "data": {
    "collectibleConnection": {
      "pageInfo": {
        "endCursor": "Zi3PY2",
        "hasNextPage": true,
        "startCursor": null,
        "hasPreviousPage": false
      },
      "nodes": [
        {
          "id": "aa961280-c28a-11ec-b21d-e1da91558163",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "waterbottle-animation-laser",
          "name": "Waterbottle Laser animation",
          "fileRel": {
            "fileId": null,
            "fileObj": {
              "cdn": "cdn.bio",
              "ext": "png",
              "prefix": "collectible/aa961280-c28a-11ec-b21d-e1da91558163"
            }
          },
          "type": "redeemable",
          "targetType": "message",
          "data": {
            "category": null,
            "redeemType": "powerup",
            "description": null,
            "redeemData": {
              "powerupId": "c80f6410-c28a-11ec-b21d-e1da91558163",
              "durationSeconds": 86400
            }
          }
        },
        {
          "id": "64de05b0-e06a-11ec-ac50-5f44841b06b9",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "ludwig-she-her",
          "name": "She/Her Flair",
          "fileRel": {
            "fileId": null,
            "fileObj": {
              "cdn": "cdn.bio",
              "ext": "png",
              "prefix": "collectible/64de05b0-e06a-11ec-ac50-5f44841b06b9"
            }
          },
          "type": "redeemable",
          "targetType": "none",
          "data": {
            "category": "flair",
            "redeemType": "powerup",
            "description": "She/Her flair",
            "redeemData": {
              "powerupId": "a75c1df0-e06a-11ec-aa23-3cf50e9492a1",
              "durationSeconds": 2678400
            }
          }
        },
        {
          "id": "cda0c990-e068-11ec-9258-7ed51e01ade1",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "ludwig-he-him",
          "name": "He/Him Flair",
          "fileRel": {
            "fileId": null,
            "fileObj": {
              "cdn": "cdn.bio",
              "ext": "png",
              "prefix": "collectible/cda0c990-e068-11ec-9258-7ed51e01ade1"
            }
          },
          "type": "redeemable",
          "targetType": "none",
          "data": {
            "category": "flair",
            "redeemType": "powerup",
            "description": "He/Him flair",
            "redeemData": {
              "powerupId": "36a195f0-e069-11ec-95fe-ca739e913d7b",
              "durationSeconds": 2678400
            }
          }
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`OwnedCollectible.collectible`

Resolves the collectible associated with an owned collectible. This is typically used to resolve the entire collectible for collectibles that a user owns

[Owned Collectible](https://www.notion.so/Owned-Collectible-4c88e35706044a4397e51a63a1771164)

***

#### Mutations

`collectibleUpsert`

Create or update a collecitble

**Directives**

`[@authOrApiAuth](<https://www.notion.so/Directives-673895108d3446118f48e9f8b881f48b>)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a collectible

```graphql
"""
Create/update a colletible
"""
collectibleUpsert(input: CollectibleUpsertInput): CollectibleUpsertPayload 
@authOrApiAuth 
@hasPermissions(filters: { collectible: { isAll: true, rank: 0 } }, action: "update")
```

**Input**

`CollectibleUpsertInput`

| Argument | Type   | Description                                                  |
| -------- | ------ | ------------------------------------------------------------ |
| id       | ID     | ID of the collectible                                        |
| slug     | String | Unique slug for the collectible                              |
| name     | String | Name of the collectible                                      |
| type     | String | Type of collectible e.g emote, discordRole, redeemable, etc. |
| data     | JSON   | Additional data for the collectible                          |

**Query**

```graphql
mutation CollectibleUpsert ($input: CollectibleUpsertInput!) {
    collectibleUpsert(input: $input) {
        collectible {
            id
            name
            type
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "a7947300-ca24-11ec-bd9c-ef3b4d5f39f9",
      "name": "pcrowBongoPlus"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "collectibleUpsert": {
      "collectible": {
        "id": "a7947300-ca24-11ec-bd9c-ef3b4d5f39f9",
        "slug": null,
        "name": "pcrowBongoPlus",
        "type": "emote"
      }
    }
  },
  "extensions": { "components": {} }
}
```
