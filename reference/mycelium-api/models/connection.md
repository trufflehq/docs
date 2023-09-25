---
description: A user connection to a 3rd party service
---

# Connection

### Resolvers

`connection`

Returns a connection

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a connection
"""
connection(input: ConnectionInput): Connection @authOrApiAuth
```

**Input**

`ConnectionInput`

| Argument          | Type   | Description                                                                   |
| ----------------- | ------ | ----------------------------------------------------------------------------- |
| sourceType        | String | Source of connection e.g twitch, youtube, etc.                                |
| sourceId          | String | ID of the source e.g twitch id, youtube id                                    |
| secondarySourceId | String | A secondary index to query for a 3rd party connection e.g twitch display name |
| orgId             | ID     | ID of the org                                                                 |
| userId            | ID     | ID of the user                                                                |

**Query**

```graphql
query ConnectionQuery ($input: ConnectionInput!) {
    connection(input: $input) {
      id
      orgId
      sourceType
      sourceId
      data
    }
}
```

**Variables**

```graphql
{
  "input": {
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
     "sourceType": "twitch",
     "sourceId": "713947004"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "connection": {
      "id": "fefa1360-5153-11ec-a089-4c0c977c6dd6",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "sourceType": "twitch",
      "sourceId": "713947004",
      "data": {
        "twitchUser": {
          "id": "713947004",
          "login": "blssouthpaw",
          "display_name": "blssouthpaw",
          "type": "",
          "broadcaster_type": "",
          "description": "",
          "profile_image_url": "https://static-cdn.jtvnw.net/user-default-pictures-uv/41780b5a-def8-11e9-94d9-784f43822e80-profile_image-300x300.png",
          "offline_image_url": "",
          "view_count": 2,
          "created_at": "2021-08-03T16:12:13Z"
        }
      }
    }
  },
  "extensions": { "components": {} }
}
```



`connectionConnection`

Returns a paginated list of connections

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a paginated list of Connections
"""
connectionsConnection(
  input: ConnectionConnectionInput,
  first: Int,
  after: String,
  last: Int,
  before: String 
): ConnectionConnection @authOrApiAuth
```

**Input**

`ConnectionConnectionInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| userId   | ID   | ID of the user |

**Query**

```graphql
query ConnectionConnectionQuery ($input: ConnectionConnectionInput, $first: Int, $after: String, $last: Int, $before: String) {
    connectionConnection(input: $input, first: $first, after: $after, last: $last, before: $before) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
            id
            orgId
            sourceType
            sourceId
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "userId": "df9efe80-cbde-11ec-9451-f79c91654543"
  },
  "first": 10
}
```

**Sample Response**

```graphql
{
  "data": {
    "connectionConnection": {
      "totalCount": 1,
      "pageInfo": { "endCursor": null, "hasNextPage": false },
      "nodes": [
        {
          "id": "b05d1ac0-cbdf-11ec-a300-96d11b6c5a3b",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "sourceType": "twitch",
          "sourceId": "713947004"
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```





### Mutations

`connectionUpsert`

Create or update a connection

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a connection

```graphql
"""
Creates/updates a connection
"""
connectionUpsert(input: ConnectionUpsertInput!): ConnectionUpsertPayload 
@authOrApiAuth
@hasPermissions(filters: { connection: { idArg: "id", rank: 0 } }, action: "update")
```

**Input**

`ConnectionUpsertInput`

| Argument   | Type   | Description                                           |
| ---------- | ------ | ----------------------------------------------------- |
| sourceType | String | Type of connection e.g twitter, twitch, youtube, etc. |
| sourceId   | String | ID of the sourceType                                  |
| orgId      | ID     | ID of the org                                         |
| userId     | ID     | ID of a user to create a connection for               |

**Query**

```graphql
mutation ConnectionUpsert ($input: ConnectionUpsertInput!) {
    connectionUpsert(input: $input) {
        connection {
            id
            orgId
            sourceType
            sourceId
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "sourceType": "custom-minecraft-smp",
    "sourceId": "f963ee10-ee21-11ec-b65b-f5593a2d1032",
    "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "connectionUpsert": {
      "connection": {
        "id": "bdb70630-ee22-11ec-ace8-1a02dbba663c",
        "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
        "sourceType": "custom-minecraft-smp",
        "sourceId": "f963ee10-ee21-11ec-b65b-f5593a2d1032"
      }
    }
  },
  "extensions": { "components": {} }
}
```



`connectionDeleteById`

Delete a connection

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _delete_ a connection

```graphql
"""
Deletes a connection
"""
connectionDeleteById(input: ConnectionDeleteByIdInput!): ConnectionDeleteByIdPayload 
@authOrApiAuth
@hasPermissions(filters: { connection: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`ConnectionDeleteByIdInput`

| Argument | Type | Description                    |
| -------- | ---- | ------------------------------ |
| id       | ID   | ID of the connection to delete |
| userId   | ID   | ID of the user                 |

**Query**

```graphql
mutation connectionDeleteById ($input: ConnectionDeleteByIdInput!) {
    connectionDeleteById (input: $input) {
        connection {
            id
            orgId
            sourceType
            sourceId
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "id": "bdb70630-ee22-11ec-ace8-1a02dbba663c"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "connectionDeleteById": {
      "connection": {
        "id": "bdb70630-ee22-11ec-ace8-1a02dbba663c",
        "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
        "sourceType": "custom-minecraft-smp",
        "sourceId": "f963ee10-ee21-11ec-b65b-f5593a2d1032"
      }
    }
  },
  "extensions": { "components": {} }
}
```

