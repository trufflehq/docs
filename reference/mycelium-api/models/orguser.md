---
description: >-
  An organization user. Users that are members of a specified organization with
  their organziation settings.
---

# OrgUser

### Resolvers

`orgUser`

Returns an orgUser

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns an OrgUser
"""
orgUser(
  input: OrgUserInput!
): OrgUser @authOrApiAuth
```

**Input**

`OrgUserInput`

| Argument | Type | Description                   |
| -------- | ---- | ----------------------------- |
| id       | ID   | ID of the orgUser             |
| userId   | ID   | ID of the user of the OrgUser |
| orgId    | ID   | ID of the org of the OrgUser  |

**Query**

```graphql
query OrgUserQuery ($input: OrgUserInput!) {
    orgUser(input: $input) {
        userId
        orgId
        roleIds
        name
        bio
        socials
        country
        state
        referrer
        hasDonated
        newsSubscribedContactMethods
        time
        orgUserCounterMap
    }
}
```

**Variables**

```graphql
{
  "input": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUser": {
      "userId": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
      "roleIds": null,
      "name": "warbyparker",
      "bio": null,
      "socials": {},
      "country": null,
      "state": null,
      "referrer": "youtube.com",
      "hasDonated": null,
      "newsSubscribedContactMethods": ["appNotification"],
      "time": "2022-03-21T16:59:42.218Z",
      "orgUserCounterMap": null
    }
  },
  "extensions": { "components": {} }
}
```



`orgUserConnection`

Returns a list of org users

**Note: pagination is still a work in progress. `first` can be used to specify the size of the result set**

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

requires permissions to _update_ the org user to be able to see the connection

```graphql
"""
Returns a list of OrgUsers

Note: Pagination is under 🚧
"""
orgUserConnection(
  input: OrgUserConnectionInput!
  first: Int
  after: String
  last: Int
  before: String
): OrgUserConnection
  @authOrApiAuth
  @hasPermissions(
    filters: { orgUser: { rank: 0 } }
    action: "update"
    usesResponse: true
    responseType: "orgUser"
  )
```

**Input**

`OrgUserConnectionInput`

| Argument     | Type    | Description                                  |
| ------------ | ------- | -------------------------------------------- |
| nameQueryStr | String  | Name of an OrgUser from a client-side search |
| query        | ESQuery | An ElasticSearch query for an OrgUser        |
| sort         | JSON    | Sort option to return an OrgUser             |

**Query**

```graphql
query OrgUserConnectionQuery ($input: OrgUserConnectionInput!) {
    orgUserConnection(input: $input) {
        totalCount
        pageInfo {
            endCursor
            hasNextPage
        }
        nodes {
           userId
            orgId
            roleIds
            name
            bio
            socials
            country
            state
            referrer
            hasDonated
            newsSubscribedContactMethods
            time
            orgUserCounterMap
        }
    }
}
```

**Variables**

```graphql
{
    "input": {
        "nameQueryStr": "ri"
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserConnection": {
      "totalCount": 1,
      "pageInfo": null,
      "nodes": [
        {
          "userId": null,
          "orgId": "5145e6a0-4199-11ec-b582-9e02ef9a0298",
          "roleIds": ["53d9ff00-4199-11ec-b8ea-a3a4280bbad3"],
          "name": "waterbottle",
          "bio": null,
          "socials": {},
          "country": null,
          "state": null,
          "referrer": null,
          "hasDonated": null,
          "newsSubscribedContactMethods": ["email", "appNotification"],
          "time": "2021-11-09T20:12:13.445Z",
          "orgUserCounterMap": { "c7831ba0-41bf-11ec-80cc-e9cdb03a1057": 3464 }
        }
      ]
    }
  },
  "extensions": { "components": {} }
}
```



`Org.orgUser`

resolves an org user for the logged in user for an org. **Requires an access token to resolve.**



`MeUser.orgUsers`

resolves a paginated list of org users for a logged in user. **Requires an access token to resolve**



`ChatMessage.orgUser`

resolves an org user from a chat message. This is used to pull info like display name tied to a chat message



`Comment.orgUser`

resolves an org user from a comment. This is usually used to pull in an org user’s info on a comment.



`Article.orgUser`

resolves an org user from an article. This is usually used to pull in an org user’s info for an article they created.



`OrgUserCounter.orgUser`

resolves an org user from an org user counter. This is usually used to pull in org user info for things like a leaderboard or a user profile.

OrgUserCounter



`Connection.orgUser`

resolves an org user from a connection. Usually used to pull in an org user’s info for a twitch, youtube, or minecraft user.

Connection





### Mutations

`orgUserSmsOptIn`

Let’s an OrgUser opt-in to SMS communications

**Directives**

`@authOrApiAuth` can read with authenticated user or a valid api key

**Permission**

must have permission to _update_ the org user

```graphql
"""
Opt-in an org user to SMS
"""
orgUserSmsOptIn: OrgUserSmsOptInPayload @authOrApiAuth @hasPermissions(
    filters: { orgUser: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`OrgUserSmsOptInInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| userId   | ID   | ID of the user |

**Query**

```graphql
mutation OrgUserSmsOptIn {
    orgUserSmsOptIn {
        isOptedIn
    }
}
```

**Sample Response**

```graphql
{
  "data": { "orgUserSmsOptIn": { "isOptedIn": true } },
  "extensions": { "components": {} }
}
```



`orgUserUpsert`

Updates an org user

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _update_ an orgUser

```graphql
"""
Updates an org user
"""
orgUserUpsert(input: OrgUserUpsertInput): OrgUserUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { orgUser: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`OrgUserUpsertInput`

| Argument    | Type   | Description                         |
| ----------- | ------ | ----------------------------------- |
| id          | ID     | ID of the org user                  |
| bio         | String | Bio for the org user                |
| socials     | JSON   | List of the socials for an org user |
| country     | String | Country of the org user             |
| region      | String | Region of the org user              |
| dateOfBirth | Date   | Date of birth for the org user      |

**Query**

```graphql
mutation OrgUserUpsert ($input: OrgUserUpsertInput) {
    orgUserUpsert(input: $input) {
       orgUser {
           id
           name
           bio
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "4d52d6a0-a938-11ec-b721-648e1609e8f2",
      "bio": "here is a new bio"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserUpsert": {
      "orgUser": {
        "id": "4d52d6a0-a938-11ec-b721-648e1609e8f2",
        "name": null,
        "bio": "here is a new bio"
      }
    }
  },
  "extensions": { "components": {} }
}
```



`orgUserSetRoleIds`

Set an org user’s assigned roles

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permissions**

must have permission to _update_ an org user

```graphql
"""
Set an org user's roles
"""
orgUserSetRoleIds(input: OrgUserSetRoleIdsInput): OrgUserSetRoleIdsPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { orgUser: { idArg: "id", rank: 0 } }
    action: "update"
  )
```

**Input**

`OrgUserSetRoleIdsInput`

| Argument | Type  | Description        |
| -------- | ----- | ------------------ |
| id       | ID    | ID of the org user |
| roleIds  | \[ID] | List of role ids   |

**Query**

```graphql
mutation OrgUserSetRolesIds ($input: OrgUserSetRoleIdsInput!) {
    orgUserSetRoleIds(input: $input) {
       orgUser {
           id
           roleIds
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "4d52d6a0-a938-11ec-b721-648e1609e8f2",
      "roleIds": [
          "53d9ff00-4199-11ec-b8ea-a3a4280bbad3",
          "53d6f1c0-4199-11ec-87ff-3a141959f16b"
      ]
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserSetRoleIds": {
      "orgUser": {
        "id": "4d52d6a0-a938-11ec-b721-648e1609e8f2",
        "roleIds": [
          "53d9ff00-4199-11ec-b8ea-a3a4280bbad3",
          "53d6f1c0-4199-11ec-87ff-3a141959f16b"
        ]
      }
    }
  },
  "extensions": { "components": {} }
}
```



`orgUserDeleteById`

Deletes an org user

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

**Permission**

must have permission to _delete_ an orgUser

```graphql
"""
Delete an org user
"""
orgUserDeleteById(input: OrgUserDeleteByIdInput!): OrgUserDeleteByIdPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { orgUser: { idArg: "id", rank: 0 } }
    action: "delete"
  )
```

**Input**

`OrgUserDeleteByIdInput`

| Argument | Type | Description        |
| -------- | ---- | ------------------ |
| id       | ID!  | ID of the org user |

**Query**

```graphql
mutation OrgUserDelete ($input: OrgUserDeleteByIdInput!) {
    orgUserDeleteById(input: $input) {
       orgUser {
           id
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
      "id": "0dd093c0-9c07-11ec-9a56-d6f218952d45"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "orgUserDeleteById": {
      "orgUser": {
        "id": "0dd093c0-9c07-11ec-9a56-d6f218952d45"
      }
    }
  },
  "extensions": { "components": {} }
}
```

