---
description: A role assigned to org users for access control
---

# Role

### Resolvers

`roleConnection`

Returns a paginated list of roles

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

requires permissions to _read_ the roles

```graphql
"""
Returns a paginated list of roles
"""
roleConnection(input: RoleConnectionInput, first: Int, after: String, last: Int, before: String): RoleConnection 
@authOrApiAuth
@hasPermissions(filters: { role: { rank: 0 } }, action: "read", usesResponse: true, responseType: "role")
```

**Input**

`RoleConnectionInput`

| Argument | Type | Description   |
| -------- | ---- | ------------- |
| orgId    | ID   | ID of the org |

**Query**

```graphql
query RoleConnectionQuery ($input: RoleConnectionInput, $first: Int, $after: String, $last: Int, $before: String) {
    roleConnection(input: $input, first: $first, after: $after, last: $last, before: $before) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
          id
          orgId
          name
          slug
          rank
          isSuperAdmin
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "roleConnection": {
      "totalCount": 2,
      "pageInfo": { "endCursor": null, "hasNextPage": false },
      "nodes": [
        {
          "id": "53d9ff00-4199-11ec-b8ea-a3a4280bbad3",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "name": "Admin",
          "slug": "admin",
          "rank": 0,
          "isSuperAdmin": true
        },
        {
          "id": "53d6f1c0-4199-11ec-87ff-3a141959f16b",
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "name": "Everyone",
          "slug": "everyone",
          "rank": 999,
          "isSuperAdmin": null
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```

***

`OrgUser.roleConnection`

Resolves a list of roles for an org user

OrgUser

***

`OrgUserInvite.roleConnection`

Resolves a list of roles tied to an org user invite

***

`Permission.role`

resolves a role for a permission. This is used to get a specific role tied to a permission

***

***

### Mutations

`roleUpsert`

Create or update a role

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a role

```graphql
"""
Create/Update a role
"""
roleUpsert(input: RoleUpsertInput): RoleUpsertPayload 
@authOrApiAuth
@hasPermissions(filters: { role: { idArg: "id", rank: 0 } }, action: "update")
```

**Input**

`RoleUpsertInput`

| Argument    | Type   | Description                                |
| ----------- | ------ | ------------------------------------------ |
| id          | ID     | ID of the role                             |
| slug        | String | Slug of the role                           |
| name        | String | Name of the role                           |
| permissions | JSON   | List of permissions for the role to update |

**Query**

```graphql
mutation RoleUpsert ($input: RoleUpsertInput!) {
    roleUpsert(input: $input) {
        role {
            id
            orgId
            name
            slug
            rank
            isSuperAdmin
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "name": "Lola's role"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "roleUpsert": {
      "role": {
        "id": "cb852d80-ee06-11ec-8d37-a5f90dcf3405",
        "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
        "name": "Lola's role",
        "slug": "lolas-role",
        "rank": null,
        "isSuperAdmin": null
      }
    }
  },
  "extensions": { "components": {} }
}
```

***

`roleSetRanks`

Update the ordering of the different ranks

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ a role

```graphql
"""
Update a list of roles' ranks
"""
roleSetRanks(input: RoleSetRanksInput): RoleSetRanksPayload
@authOrApiAuth
@hasPermissions(filters: { role: { idArg: "id", rank: 0 } }, action: "update")
```

**Input**

`RoleSetRanksInput`

| Argument | Type  | Description                     |
| -------- | ----- | ------------------------------- |
| ids      | \[ID] | ID of roles to update ranks for |

**Query**

```graphql
mutation RoleSetRanks ($input: RoleSetRanksInput!) {
    roleSetRanks(input: $input) {
        isUpdated
    }
}
```

**Variables**

```graphql
{
  "input": {
    "ids": [
        "53d9ff00-4199-11ec-b8ea-a3a4280bbad3",
        "cb852d80-ee06-11ec-8d37-a5f90dcf3405",
        "53d6f1c0-4199-11ec-87ff-3a141959f16b"
    ]
  }
}
```

**Sample Response**

```graphql
{
  "data": { "roleSetRanks": { "isUpdated": true } },
  "extensions": { "components": {} }
}
```

***

`roleDeleteById`

Delete a role

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _delete_ a role

```graphql
"""
Delete a role
"""
roleDeleteById(input: RoleDeleteByIdInput!): RoleDeleteByIdPayload 
@authOrApiAuth
@hasPermissions(filters: { role: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`RoleDeleteByIdInput`

| Argument | Type | Description              |
| -------- | ---- | ------------------------ |
| id       | ID   | ID of the role to delete |

**Query**

```graphql
mutation RoleDeleteById ($input: RoleDeleteByIdInput!) {
    roleDeleteById(input: $input) {
        role {
            id
            orgId
            name
            slug
            rank
            isSuperAdmin
        }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "id": "cb852d80-ee06-11ec-8d37-a5f90dcf3405"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "roleDeleteById": {
      "role": {
        "id": "cb852d80-ee06-11ec-8d37-a5f90dcf3405",
        "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
        "name": "Lola's role",
        "slug": "lolas-role",
        "rank": 1,
        "isSuperAdmin": null
      }
    }
  },
  "extensions": { "components": {} }
}
```

***
