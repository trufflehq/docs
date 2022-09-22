---
description: A powerup that can be applied to a user or an entity like an article
---

# Powerup

### Resolvers

`powerup`

Returns a powerup

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permissions**

requires permissions to `read` the powerup

```graphql
"""
  Returns a Powerup
  """
  powerup(input: PowerupInput): Powerup @authOrApiAuth @hasPermissions(filters: { powerup: { idArg: "id", rank: 0 } }, action: "read")
```

**Input**

`PowerupInput`

| Argument | Type | Description       |
| -------- | ---- | ----------------- |
| id       | ID   | ID of the powerup |

**Query**

```graphql
query PowerupQuery ($input: PowerupInput) {
    powerup(input: $input) {
        id
        orgId
        slug
        name
        jsx
        componentRels {
            component {
                id
                packageVersionId
            }
        }
        data
    }
}
```

**Variables**

```graphql
{
   "input": {
       "id": "36a195f0-e069-11ec-95fe-ca739e913d7b"
   }
}
```

**Sample Response**

```graphql
{
  "data": {
    "powerup": {
      "id": "36a195f0-e069-11ec-95fe-ca739e913d7b",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "slug": "ludwig-he-him",
      "name": "He/Him Flair",
      "jsx": "<Component\n  slug=\"flair\"\n  props={{\n    imageSrc: \"https://cdn.bio/ugc/collectible/cda0c990-e068-11ec-9258-7ed51e01ade1.small.png\",\n    type: 'png'\n  }}\n/>",
      "componentRels": [{ "component": null }],
      "data": {}
    }
  },
  "extensions": { "components": {} }
}
```

***

`powerupConnection`

Returns a paginated list of powerups for an org

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { powerup: { idArg: "id", rank: 0 } }, action: "read")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

**Query**

```graphql
query PowerupConnectionQuery ($first: Int, $after: String) {
    powerupConnection(first: $first, after: $after) {
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
            id
            orgId
            slug
            name
            jsx
            componentRels {
                component {
                    id
                    packageVersionId
                }
            }
            data
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
    "powerupConnection": {
      "pageInfo": { "endCursor": "1Uj0Ex", "hasNextPage": true },
      "nodes": [
        {
          "id": "b2d8e190-579e-11ec-97d5-e55be0da4948",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "stanz-flair-santa",
          "name": "Stanz Santa Flair",
          "jsx": "<Component\n      slug=\"flair\"\n      props={{\n        imageSrc: \"https://cdn.bio/assets/images/creators/stanz/powerups/flair_santa.svg?2\"\n      }}\n    />",
          "componentRels": [{ "component": null }],
          "data": {}
        },
        {
          "id": "19dafee0-583b-11ec-97d5-e55be0da4948",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "stanz-flair-snowflake",
          "name": "Stanz Snowflake Flair",
          "jsx": "<Component\n      slug=\"flair\"\n      props={{\n        imageSrc: \"https://tdn.one/assets/images/spore/emotes/snowflake.svg\"\n      }}\n    />",
          "componentRels": [{ "component": null }],
          "data": {}
        },
        {
          "id": "01c52670-5848-11ec-97d5-e55be0da4948",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "stanz-animation-squirm",
          "name": "Stanz Squirm powerup (24hr)",
          "jsx": "<Component\n      slug=\"message-animation\"\n      props={{\n        imageSrc: \"https://cdn.bio/assets/images/creators/stanz/powerups/animation_stanz_squirm.svg?1\"\n      }}\n    />",
          "componentRels": [{ "component": null }],
          "data": {
            "color": "#8b32a8",
            "colorText": "#ffffff",
            "layoutClass": "background-right-on-wide"
          }
        },
        {
          "id": "0643f7d0-5848-11ec-97d5-e55be0da4948",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "stanz-animation-staniel-sherbert",
          "name": "Staniel Sherbert powerup (24hr)",
          "jsx": "<Component\n      slug=\"message-animation\"\n      props={{\n        imageSrc: \"https://cdn.bio/assets/images/creators/stanz/powerups/animation_staniel_sherbert.svg\"\n      }}\n    />",
          "componentRels": [{ "component": null }],
          "data": {
            "color": "#f48d42",
            "colorText": "#ffffff",
            "layoutClass": "background-right-on-wide"
          }
        },
        {
          "id": "6e9d7140-6378-11ec-92fe-132e7017c79a",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "slug": "stanz-animation-sheesh",
          "name": "Sheesh powerup (24hr)",
          "jsx": "<>\n      <Component\n        slug=\"message-animation\"\n        props={{\n          imageSrc: \"https://cdn.bio/assets/images/features/powerups/animation_sheesh.svg\",\n        }}\n      />\n      <div className=\"background\" style={{\n        background: 'url(https://cdn.bio/assets/images/creators/stanz/powerups/sheesh.png)',\n        position: 'absolute',\n        top: 0,\n        left: 0,\n        width: '100%',\n        height: '100%',\n        'background-size': 'auto 100%',\n        'background-repeat': 'no-repeat',\n        'background-position': 'center'\n      }} />\n    </>",
          "componentRels": [{ "component": null }],
          "data": {
            "color": "#ff2828",
            "colorText": "#ffffff",
            "layoutClass": "bottom"
          }
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`Collectible.powerup`

Resolves a powerup from a collectible based on it’s `data.redeemType`. The collectible format usually follows:

```jsx
collectible: {
 ...
 data: {
   redeemType: 'powerup',
   redeemData: {
		powerupId: '<powerupId>'
   }
 }
}
```

Collectible

***

`ActivePowerup.powerup`

Resolves a powerup from an active powerup. This query is usually used to resolve the backing powerup data for a user’s active powerup. e.g how long the powerup is active, if there’s any additional data tied to the powerup that needs to be rendered in the UI.

Active Powerup

***

### Mutations

`powerupUpsert`

Create or update a powerup

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

Must have permission to update a powerup

**Input**

`PowerupUpsertInput`

| Argument | Type   | Description                                        |
| -------- | ------ | -------------------------------------------------- |
| id       | ID     | ID of the powerup                                  |
| name     | String | Name of the powerup                                |
| slug     | String | Slug of the powerup                                |
| jsx      | String | JSX associated w/ the powerup that can be rendered |
| data     | JSON   | Associated data for the powerup                    |

**Query**

```graphql
mutation PowerupUpsert ($input: PowerupUpsertInput!) {
    powerupUpsert(input: $input) {
       powerup {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "name": "Epic Flair",
      "slug": "org-epic-flair",
      "jsx": "<Component\n      slug=\"flair\"\n      props={{\n        imageSrc: \"https://tdn.one/assets/images/spore/emotes/epicFlair.svg\"\n      }}\n    />",
      "data": {}
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "powerupUpsert": {
      "powerup": { "id": "c74f9600-ed49-11ec-a5aa-be1ee1661992" }
    }
  },
  "extensions": { "components": {} }
}
```
