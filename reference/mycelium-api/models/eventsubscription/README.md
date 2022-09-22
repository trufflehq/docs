---
description: >-
  An event subscription that allows 3rd parties to receive events created
  through Truffle
---

# EventSubscription

### Resolvers

`eventSubscription`

Returns an event subscription

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns an event subscription
"""
eventSubscription(input: EventSubscriptionInput): EventSubscription @authOrApiAuth
```

**Input**

`EventSubscriptionInput`

| Argument | Type | Description                  |
| -------- | ---- | ---------------------------- |
| id       | ID   | ID of the event subscription |

**Query**

```graphql
query EventSubscription ($input: EventSubscriptionInput) {
    eventSubscription(input: $input) {
        id
        eventTopicId
        actionRel {
            action {
                id
                packageVersionId
            }
            actionId
        }
    }
}
```

**Variables**

```graphql
{
    "input": {
        "id": "8f87a0c0-fc01-11ec-867e-a487913361f8"
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

`eventSubscriptionConnection`

Returns a paginated list of event subscriptions

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of event subscriptions
"""
eventSubscriptionConnection(first: Int, after: String, last: Int, before: String): EventSubscriptionConnection 
@authOrApiAuth
```

**Query**

```graphql
query EventSubscriptionConnection ($first: Int, $after: String, $last: Int, $before: String) {
    eventSubscriptionConnection(first: $first, after: $after, last: $last, before: $before) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
            id
            status
            actionRel {
                action {
                    id
                    type
                }
                runtimeData
            }
          
        }
    }
}
```

**Variables**

```graphql
{}
```

**Sample Response**

```graphql
{
    "data": {
        "eventSubscriptionConnection": {
            "totalCount": 4,
            "pageInfo": {
                "endCursor": null,
                "hasNextPage": false
            },
            "nodes": [
                {
                    "id": "817a42d0-f986-11ec-bcd9-d7e7af9d36c8",
                    "status": "online",
                    "actionRel": {
                        "action": {
                            "id": "841dcaf0-f8ca-11ec-81b7-efe9af51d4b7",
                            "type": "webhook"
                        },
                        "runtimeData": {
                            "endpoint": "<url>"
                        }
                    }
                }
								...
            ]
        }
    },
    "extensions": {
        "components": {}
    }
}
```

***

***

### Mutations

`eventSubscriptionUpsert`

Create or updates an event subscription

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { eventSubscription: { isAll: true, rank: 0 } }, action: "update")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to update an event subscription

```graphql
"""
Create or updates an event subscription
"""
eventSubscriptionUpsert(input: EventSubscriptionUpsertInput!): EventSubscriptionUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { eventSubscription: { isAll: true, rank: 0 } }
    action: "update"
  )
```

**Input**

`EventSubscriptionUpsertInput`

| Argument       | Type           | Description                                                     |
| -------------- | -------------- | --------------------------------------------------------------- |
| eventTopicPath | String         | The event topic path you'd like to subscribe to                 |
| actionRel      | ActionRelInput | Object containing action id/path and runtimeData to send action |

🕯️ If you’re executing this query with a package API key. Make sure the package has been installed on the development org and has the proper permissions

```jsx
{
  filters: { eventSubscription: { isAll: true, rank: 0 } },
  action: "update",
  value: true,
},
```

**Query**

```graphql
mutation EventSubscriptionUpsert ($input: EventSubscriptionUpsertInput!) {
    eventSubscriptionUpsert(input: $input) {
        eventSubscription {
            id
            eventTopicId
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "eventTopicPath": "@truffle-dev-early-access/riley-event-sub-test@latest/_EventTopic/rm-new-event-sub-topic",
      "actionRel": {
          "actionPath": "@truffle/core@1.0.0/_Action/webhook",
          "runtimeData": {
              "endPoint": "https://c4b4-98-142-186-46.ngrok.io/truffle/webhook"
          }
      }
  }
}
```

**Sample Response**

```graphql
{
    "data": {
        "eventSubscriptionUpsert": {
            "eventSubscription": {
                "id": "1b01ca90-fc9d-11ec-8aa7-5a444feacd51",
                "eventTopicId": "16398990-fc9c-11ec-9681-85ea14fe2e0b"
            }
        }
    },
    "extensions": {
        "components": {}
    }
}
```

***

`eventSubscriptionDelete`

Delete an event subscription

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { eventSubscription: { idArg: "id", rank: 0 } }, action: "delete")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to delete the specific event subscription

```graphql
"""
Delete an event subscription
"""
eventSubscriptionDelete(input: EventSubscriptionDeleteInput!): EventSubscriptionDeletePayload
  @authOrApiAuth
  @hasPermissions(
    filters: { eventSubscription: { idArg: "id", rank: 0 } }
    action: "delete"
  )
```

**Input**

`EventSubscriptionDeleteInput`

| Argument | Type | Description                  |
| -------- | ---- | ---------------------------- |
| id       | ID   | ID of the event subscription |

🕯️ If you’re executing this query with a package API key. Make sure the package has been installed on the development org and has the proper permissions

```jsx
{
  filters: { eventSubscription: { isAll: true, rank: 0 } },
  action: "delete",
  value: true,
},
```

**Query**

```graphql
mutation EventSubscriptionDelete ($input: EventSubscriptionDeleteInput!) {
    eventSubscriptionDelete(input: $input) {
       eventSubscription {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "7714ba70-f3da-11ec-8b62-20ffc9659e62"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "eventSubscriptionDelete": {
      "eventSubscription": {
        "id": "7714ba70-f3da-11ec-8b62-20ffc9659e62"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***
