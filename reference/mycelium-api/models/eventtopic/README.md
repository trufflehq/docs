---
description: A topic that is emitted to signify an event has happened inside of Truffle
---

# EventTopic

### Resolvers

***

### Mutations

`eventTopicUpsert`

Create or update an event topic

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { eventTopic: { isAll: true, rank: 0 } }, action: "update")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to update an event topic

```graphql
"""
Create or update an event topic
"""
eventTopicUpsert(input: EventTopicUpsertInput!): EventTopicUpsertPayload 
	@authOrApiAuth
  @hasPermissions(
    filters: { eventTopic: { isAll: true, rank: 0 } }
    action: "update"
  )
```

**Input**

`EventTopicUpsertInput`

| Argument         | Type   | Description                                    |
| ---------------- | ------ | ---------------------------------------------- |
| slug             | String | The string representation of the topic         |
| packageVersionId | ID     | ID of the package version the topic belongs to |

Not for this query, if you’re using a package api key make sure the package has been installed with

```json
{
  filters: { eventTopic: { isAll: true, rank: 0 } },
  action: "update",
  value: true,
}
```

as a requested permission so that package has permission to create the event topic.

**Query**

```graphql
mutation EventTopicUpsert ($input: EventTopicUpsertInput!) {
    eventTopicUpsert(input: $input) {
        eventTopic {
            id
            orgId
            packageVersionId
            slug
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "slug": "rm-new-event-sub-topic"
  }
}
```

**Sample Response**

```graphql
{
    "data": {
        "eventTopicUpsert": {
            "eventTopic": {
                "id": "16398990-fc9c-11ec-9681-85ea14fe2e0b",
                "orgId": "661a4190-ee94-11ec-8ff4-bbfb3e013d43",
                "packageVersionId": "fe751860-fc9b-11ec-a2f6-d46c35cf0391",
                "slug": "rm-new-event-sub-topic"
            }
        }
    },
    "extensions": {
        "components": {}
    }
}
```

***
