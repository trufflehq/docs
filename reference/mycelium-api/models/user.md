---
description: A Truffle User across all orgs
---

# User

### Resolvers

`me`

Returns logged in user

**Directives**

`[@auth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user. **Requires a user access token for this query**

```graphql
"""
Returns the logged in user
"""
me: MeUser @auth
```

**Query**

```graphql
query UserGetMe {
    me {
      id
      name
      email
      time
      country
      hasStripeId
      hasPassword
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "me": {
      "id": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "name": "warbyparker",
      "email": "warbyparker@spore.build",
      "time": null,
      "country": null,
      "hasStripeId": false,
      "hasPassword": true
    }
  },
  "extensions": { "components": {} }
}
```

***

`user`

Returns a user

**Directives**

`@authOrApiAuth` can read with authenticated user or valid api key

```graphql
"""
Returns a user
"""
user(input: UserInput): User @authOrApiAuth
```

**Input**

`UserInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| id       | ID   | ID of the user |

**Query**

```graphql
query UserById ($input: UserInput) {
    user(input: $input) {
      id
      name
      time
    }
}
```

**Variables**

```graphql
{
    "input": {
        "id": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7"
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "user": {
      "id": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
      "name": "warbyparker",
      "time": "2022-03-21T16:59:41.034Z"
    }
  },
  "extensions": { "components": {} }
}
```

***

`users`

Returns a list of users

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a list of users
"""
users(input: UsersInput): [User] @authOrApiAuth
```

**Input**

`UsersInput`

| Argument | Type  | Description      |
| -------- | ----- | ---------------- |
| ids      | \[ID] | List of user IDs |

**Query**

```graphql
query UsersByIds ($input: UsersInput) {
    users(input: $input) {
      id
      name
      time
    }
}
```

**Variables**

```graphql
{
    "input": {
        "ids": [
					"4c9e2ca0-a938-11ec-8d59-a137801ecbe7", 
					"9158bf00-a946-11ec-aba9-953e43ac90bf"
				]
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "users": [
      {
        "id": "4c9e2ca0-a938-11ec-8d59-a137801ecbe7",
        "name": "warbyparker",
        "time": "2022-03-21T16:59:41.034Z"
      },
      {
        "id": "9158bf00-a946-11ec-aba9-953e43ac90bf",
        "name": "macncheese",
        "time": "2022-03-21T18:41:49.296Z"
      }
    ]
  },
  "extensions": { "components": {} }
}
```

***

`OrgUser.user`

resolves a user from an org user. This is used to grab the Truffle user associated with an org user.

OrgUser

***

`Chat.users`

resolves a list of all of the users in a chat (channel or dm).

***

`Comment.user`

resolves a user from one of their comments

***

`Donation.user`

resolves a user from a donation.

***

`FormResponse.user`

resolves a user from one of their responses to a form.

FormResponse

***

`OrgUserCounter.user`

resolves a user from an org user counter. This is usually used to grab a user when pulling a leaderboard or user profile.

OrgUserCounter

***

`Alert.user`

resolves a user from an alert.

***

***

### Mutations

`userLoginAnon`

An anonymous login to get an initial user and access token

**Directives**

None

```graphql
"""
Anonymous user login for when a user first arrives at a site
"""
userLoginAnon: UserLoginAnonPayload
```

**Query**

```graphql
mutation UserLoginAnon {
    userLoginAnon {
       accessToken
    }
}
```

**Sample Response**

```graphql
{
  "data": {
    "userLoginAnon": {
      "accessToken": "an access token"
    }
  },
  "extensions": { "components": {} }
}
```

***

`userJoin`

Mutation for a user to signup

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can call with authenticated user or valid api key

```graphql
"""
User signup
"""
userJoin(
  input: UserJoinInput!
): UserJoinPayload @authOrApiAuth
```

**Input**

`UserJoinInput`

| Argument       | Type    | Description                                |
| -------------- | ------- | ------------------------------------------ |
| name           | String  | Name of the user                           |
| email          | String  | Email of the user                          |
| phone          | String  | Phone number of the user                   |
| password       | String  | Password of the user                       |
| hasSmsConsent  | Boolean | Whether the user has opted into sms or not |
| inviteTokenStr | String  | An invite string                           |
| referrer       | String  | Where the user was referred from           |
| source         | String  | Source of where the user was referred from |
| userId         | ID      | ID of the user                             |

**Query**

```graphql
mutation UserJoin ($input: UserJoinInput!) {
    userJoin(input: $input) {
       accessToken
    }
}
```

**Variables**

```graphql
{
  "input": {
    "name": "lola",
    "email": "lolasleepy@spore.build",
    "password": "lolasleepy1234abc"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "userJoin": {
      "accessToken": "an access token"
    }
  },
  "extensions": { "components": {} }
}
```

***

`userLoginEmailPhone`

User login with an email or phone number

**Directives**

None

```graphql
"""
User login
"""
userLoginEmailPhone(
  input: UserLoginEmailPhoneInput!
): UserLoginEmailPhonePayload
```

**Input**

`UserLoginEmailPhoneInput`

| Argument | Type   | Description              |
| -------- | ------ | ------------------------ |
| email    | String | Email of the user        |
| phone    | String | Phone number of the user |
| password | String | Password of the user     |

**Query**

```graphql
mutation UserLoginEmailPhone ($input: UserLoginEmailPhoneInput!) {
    userLoginEmailPhone(input: $input) {
       accessToken {
           accessToken
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "email": "lolasleepy@spore.build",
    "password": "lolasleepy1234abc"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "userLoginEmailPhone": {
      "accessToken": {
        "accessToken": "an access token"
      }
    }
  },
  "extensions": { "components": {} }
}
```

***

`userSetName`

Set an anonymous user’s name

**Directives**

None

```graphql
"""
Set a username
"""
userSetName(input: UserSetNameInput!): UserSetNamePayload
@authOrApiAuth
```

**Input**

`UserSetNameInput`

| Argument | Type   | Description                    |
| -------- | ------ | ------------------------------ |
| name     | String | Name of the user               |
| referrer | String | website that referred the user |
| source   | String | source of the user             |

**Query**

```graphql
mutation UserSetName ($input: UserSetNameInput!) {
    userSetName(input: $input) {
       user {
           name
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "name": "lolasleepy",
    "referrer": "pets.com"
  }
}
```

**Sample Response**

```graphql
{
  "data": { "userSetName": { "user": { "name": "lolasleepy" } } },
  "extensions": { "components": {} }
}
```

***

`userUpsert`

Use to update a user and to create a new password

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Update a user's information
"""
userUpsert(
  input: UserUpsertInput
): UserUpsertPayload @authOrApiAuth
```

**Input**

`UserUpsertInput`

| Argument         | Type   | Description                     |
| ---------------- | ------ | ------------------------------- |
| name             | String | name of the user                |
| email            | String | Email of the user               |
| phone            | String | Phone number of the user        |
| password         | String | New password of the user        |
| currentPassword  | String | Current password of the user    |
| passwordResetKey | String | Nonce sent from the reset email |
| userId           | ID     | ID of the user                  |

**Query**

```graphql
mutation UserUpsert ($input: UserUpsertInput!) {
    userUpsert(input: $input) {
       user {
           name
           email
       }
    }
}
```

**Variables**

```graphql
{
  "input": {
    "name": "lolasleepy@spore.build",
    "currentPassword": "lolaawakendr1234abc",
    "password": "lolaawakendrr1234abc"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "userUpsert": {
      "user": {
        "name": "lolasleepy@spore.build",
        "email": "lolasleepy@spore.build"
      }
    }
  },
  "extensions": { "components": {} }
}
```

***
