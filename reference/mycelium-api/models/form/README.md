---
description: Forms are used to organize questions and responses.
---

# Form

### Resolvers

`form`

Returns a form

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

requires permissions to read the form

```graphql
"""
Returns a Form
"""
form(input: FormInput): Form @authOrApiAuth
```

**Input**

`FormInput`

| Argument | Type   | Description       |
| -------- | ------ | ----------------- |
| id       | ID     | ID of the form    |
| slug     | String | Slug for the form |

**Query**

```graphql
query GetForm($input: FormInput!) {
  form(input: $input) {
    id
    orgId
    slug
    name
    data
    description
    maxResponsesPerUser
    endTime
    formQuestionConnection {
      nodes {
        id
        question
      }
    }
    formResponseConnection(first: 10) {
      nodes {
        formQuestionAnswerConnection {
          nodes {
            value
          }
        }
      }
    }
  }
}
```

**Variables**

```graphql
{
  "input": {
    "id": "6612c7a0-0305-11ed-8f41-738b1c48eaac"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "form": {
      "id": "6612c7a0-0305-11ed-8f41-738b1c48eaac",
      "orgId": "e2853b00-0243-11ed-bf99-3b2dd8713144",
      "slug": "my-first-form",
      "name": "My first form",
      "data": {
        "something": "useful"
      },
      "description": "The first form that I intend to send to my audience.",
      "maxResponsesPerUser": 1,
      "endTime": "2022-07-17T00:00:00.000Z",
      "formQuestionConnection": {
        "nodes": []
      },
      "formResponseConnection": {
        "nodes": []
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formConnection`

Returns a list of forms

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

\*`[@hasPermissions*(filters: { form: { rank: 0 } }, action: "read", usesResponse: true, responseType: "form")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

requires permissions to read the powerup

```graphql
"""
Returns a paginated list of Forms
"""
formConnection(first: Int, after: String, last: Int, before: String): FormConnection
  @authOrApiAuth
  @hasPermissions(
    filters: { form: { rank: 0 } }
    action: "read"
    usesResponse: true
    responseType: "form"
  )
```

**Input**

| Argument | Type | Description                      |
| -------- | ---- | -------------------------------- |
| orgId    | ID   | ID of the org to query forms for |

**Query**

```graphql
query GetForms {
  formConnection {
    nodes {
      id
      name
      slug
    }
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "formConnection": {
      "nodes": [
        {
          "id": "fa6dfd10-0243-11ed-b5e9-db087a3c304f",
          "name": "Test form",
          "slug": "test-form"
        },
        {
          "id": "51498750-0300-11ed-b368-04537124a810",
          "name": "My first form",
          "slug": "my-first-form"
        },
        ...
      ]
    }
  },
  "extensions": {
    "components": {}
  }
}
```



### Mutations

`formUpsert`

Create or update a form

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { form: { isAll: true, rank: 0 } }, action: "create")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

```graphql
"""
Creates/updates a form
"""
formUpsert(input: FormUpsertInput!): FormUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { form: { isAll: true, rank: 0 } }
    action: "create"
  )
```

**Input**

`FormUpsertInput`

| Argument            | Type   | Description                                           |
| ------------------- | ------ | ----------------------------------------------------- |
| id                  | ID     | ID of the powerup                                     |
| orgId               | ID     | The ID of the org the Form is hosted on               |
| name                | String | The name of the Form                                  |
| data                | JSON   | Additional data associated with the form (buttonText) |
| description         | String | A description of the form                             |
| maxResponsesPerUser | Int    | The max number of times a user can submit             |
| endTime             | Date   | Date the form should close                            |

**Query**

```graphql
mutation FormUpsert($input: FormUpsertInput!) {
  formUpsert(input: $input) {
   form {
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
    "name": "My first form"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "formUpsert": {
      "form": {
        "id": "1bfe5a40-0304-11ed-be25-f17dee6341b8",
        "name": "My first form"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formDeleteById`

Deletes a form with a specified id

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { form: { idArg: "id", rank: 0 } }, action: "delete")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to update a form

```graphql
"""
Deletes a form
"""
formDeleteById(input: FormDeleteByIdInput!): FormDeleteByIdPayload
	@authOrApiAuth
	@hasPermissions(filters: { form: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`FormDeleteByIdInput`

| Argument | Type | Description    |
| -------- | ---- | -------------- |
| id       | ID   | ID of the form |

**Query**

```graphql
mutation DeleteForm($input: FormDeleteByIdInput!) {
  formDeleteById(input: $input) {
    form {
      id
    }
  }
}
```

**Variables**

```graphql
{
  "input": {
    "id": "6cc0c750-0300-11ed-8b12-68e2b34c9b64"
  }
}
```

**Sample Response**

```graphql
{
  "data": {
    "formDeleteById": {
      "form": {
        "id": "6cc0c750-0300-11ed-8b12-68e2b34c9b64"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

