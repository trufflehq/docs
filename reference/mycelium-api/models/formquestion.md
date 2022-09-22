---
description: Represents a question in a form.
---

# FormQuestion

### Resolvers

`formQuestion`

Returns a `FormQuestion`.

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

```graphql
"""
Returns a form question
"""
formQuestion(input: FormQuestionInput): FormQuestion @authOrApiAuth
```

**Input**

`FormQuestionInput`

| Argument | Type | Description            |
| -------- | ---- | ---------------------- |
| id       | ID   | ID of the FormQuestion |

**Query**

```graphql
query GetFormQuestion($input: FormQuestionInput!) {
  formQuestion(input: $input) {
    id
    orgId
    formId
    question
    type
    data
  }
}
```

**Variables**

```graphql
{
  "input": {
    "id": "bf8b8ed0-03bd-11ed-ad4a-d22d97f87fff"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestion": {
      "id": "bf8b8ed0-03bd-11ed-ad4a-d22d97f87fff",
      "orgId": "acd9d230-b9dd-11ec-bc90-7b62339255c4",
      "formId": "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
      "question": "What is your favorite color?",
      "type": "shortText",
      "data": {
        "something": "useful"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***

`formQuestionConnection`

Returns a list of `FormQuestion`s.

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestion: { rank: 0 } }, action: "read", usesResponse: true, responseType: "formQuestion")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

requires permissions to read the FormQuestion

```graphql
"""
Returns a paginated list of form questions
"""
formQuestionConnection(first: Int, after: String, last: Int, before: String): FormQuestionConnection
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestion: { rank: 0 } }
    action: "read"
    usesResponse: true
    responseType: "formQuestion"
  )
```

**Input**

`FormQuestionConnectionInput`

| Argument | Type | Description                              |
| -------- | ---- | ---------------------------------------- |
| orgId    | ID   | ID of the org to query FormQuestions for |

**Query**

```graphql
query GetFormQuestions {
  formQuestionConnection {
    nodes {
      id
      question
    }
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionConnection": {
      "nodes": [
        {
          "id": "517dd000-02fb-11ed-929d-5b59cc41d708",
          "question": "What is your favorite color?"
        },
        {
          "id": "d22a7950-02f7-11ed-a2e8-275b9a9a7624",
          "question": "What is your favorite food?"
        },
        {
          "id": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
          "question": "What is your favorite animal?"
        }
      ]
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***

### Mutations

`formQuestionUpsert`

Create or update a `FormQuestion`

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`@hasPermissions(filters: { formQuestion: { isAll: true, rank: 0 } }, action: "create")` must have permissions to write to the FormQuestion

```graphql
"""
Creates/updates a form question
"""
formQuestionUpsert(input: FormQuestionUpsertInput!): FormQuestionUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestion: { isAll: true, rank: 0 } }
    action: "create"
  )
```

**Input**

`FormQuestionUpsertInput`

| Argument | Type   | Description                                                                      |
| -------- | ------ | -------------------------------------------------------------------------------- |
| id       | ID     | ID of a FormQuestion                                                             |
| formId   | ID     | ID of the Form that the FormQuestion belongs to. Cannot be updated after insert. |
| question | String | The question                                                                     |
| type     | String | The type of FormQuestion (shortText                                              |
| data     | JSON   | Additional data associated with a FormQuestion                                   |

**Query**

```graphql
mutation CreateFormQuestion($input: FormQuestionUpsertInput!) {
  formQuestionUpsert(input: $input) {
    formQuestion {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "formId": "1d6f7fc0-0620-11ed-81c2-29ddd4e34db3",
    "formQuestions": [
      {
        "id": "b66cb0d0-0620-11ed-99a7-dd03a6c7efef",
        "question": "Do you have a driver's license?"
      },
      {
        "id": "b66b2a30-0620-11ed-999f-3459b07bff6f",
        "question": "What is your age?"
      }
    ]
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionBatchUpsert": {
      "formQuestions": [
        {
          "id": "b66cb0d0-0620-11ed-99a7-dd03a6c7efef",
          "question": "Do you have a driver's license?",
          "type": "shortText"
        },
        {
          "id": "b66b2a30-0620-11ed-999f-3459b07bff6f",
          "question": "What is your age?",
          "type": "shortText"
        }
      ]
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***

`formQuestionBatchUpsert`

Batch upserts a list of form questions

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestion: { isAll: true, rank: 0 } }, action: "create")](FormQuestion%20ec1cfb2f4b294a8691e0eb01bbfcd70e.md)`

```graphql
formQuestionBatchUpsert(
	input: FormQuestionBatchUpsertInput!
): FormQuestionBatchUpsertPayload
    @authOrApiAuth
    @hasPermissions(
      filters: { formQuestion: { isAll: true, rank: 0 } }
      action: "create"
    )
```

**Input**

`FormQuestionBatchUpsertInput`

| Argument      | Type                          | Description                         |
| ------------- | ----------------------------- | ----------------------------------- |
| formId        | ID                            | ID of the form                      |
| formQuestions | \[FormQuestionBatchUpsertRow] | The list of formQuestions to upsert |

`FormQuestionBatchUpsertRow`

| Argument | Type   | Description                                    |
| -------- | ------ | ---------------------------------------------- |
| id       | ID     | ID of a FormQuestion                           |
| question | String | The question                                   |
| type     | String | The type of FormQuestion (shortText            |
| data     | JSON   | Additional data associated with a FormQuestion |

**Query**

```graphql
mutation BatchUpsertFormQuestions($input: FormQuestionBatchUpsertInput!) {
  formQuestionBatchUpsert(input: $input) {
    formQuestions {
      id
      question
      type
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "formId": "1d6f7fc0-0620-11ed-81c2-29ddd4e34db3",
    "formQuestions": [
      {
        "question": "Do you have a driver's license?"
      },
      {
        "question": "What is your age?"
      }
    ]
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionBatchUpsert": {
      "formQuestions": [
        {
          "id": "b66cb0d0-0620-11ed-99a7-dd03a6c7efef",
          "question": "Do you have a driver's license?",
          "type": "shortText"
        },
        {
          "id": "b66b2a30-0620-11ed-999f-3459b07bff6f",
          "question": "What is your age?",
          "type": "shortText"
        }
      ]
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***

`formQuestionDeleteById`

Delete a `FormQuestion`

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestion: { idArg: "id", rank: 0 } }, action: "delete")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

```graphql
"""
Deletes a form question
"""
formQuestionDeleteById(input: FormQuestionDeleteByIdInput!): FormQuestionDeleteByIdPayload
  @authOrApiAuth
  @hasPermissions(filters: { formQuestion: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`FormQuestionDeleteByIdInput`

| Argument | Type | Description             |
| -------- | ---- | ----------------------- |
| id       | ID   | ID of the form question |

**Query**

```graphql
mutation DeleteFormQuestion($input: FormQuestionDeleteByIdInput!) {
  formQuestionDeleteById(input: $input) {
    formQuestion {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "id": "d22a7950-02f7-11ed-a2e8-275b9a9a7624"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionDeleteById": {
      "formQuestion": {
        "id": "d22a7950-02f7-11ed-a2e8-275b9a9a7624"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

***
