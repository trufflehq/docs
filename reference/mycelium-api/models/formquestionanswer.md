---
description: Represents a user’s answer to a question. It belongs to a form.
---

# FormQuestionAnswer

### Resolvers

`formQuestionAnswer`

Returns a form question answer

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestionAnswer: { rank: 0 } }, action: "read", usesResponse: true, responseType: "formQuestionAnswer")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

requires permissions to read the FormQuestionAnswer

```graphql
"""
Returns a form question answer
"""
formQuestionAnswer(input: FormQuestionAnswerInput!): FormQuestionAnswer
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestionAnswer: { rank: 0 } }
    action: "read"
    usesResponse: true
    responseType: "formQuestionAnswer"
  )
```

**Input**

`FormQuestionAnswerInput`

| Argument | Type | Description                  |
| -------- | ---- | ---------------------------- |
| id       | ID   | ID of the FormQuestionAnswer |

**Query**

```graphql
query GetFormQuestionAnswer($input: FormQuestionAnswerInput!) {
  formQuestionAnswer(input: $input) {
    id
    formQuestionId
    formResponseId
    value
    metadata
  }
}
```

**Variables**

```json
{
  "input": {
    "id": "ca5e2750-047b-11ed-9b24-395b16e1847c"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionAnswer": {
      "id": "ca5e2750-047b-11ed-9b24-395b16e1847c",
      "formQuestionId": "be823770-0244-11ed-bbb5-764d11f7aa65",
      "formResponseId": "173917b0-03cd-11ed-8edc-6a52fcd0029a",
      "value": "Chicken",
      "metadata": {
        "something": "useful"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formQuestionAnswerConnection`

Returns a list of `FormQuestionAnswer`s.

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestionAnswer: { rank: 0 } }, action: "read", usesResponse: true, responseType: "formQuestionAnswer")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

requires permissions to read the `FormQuestionAnswer`

```graphql
"""
Returns a paginated list of answers to questions in a form
"""
formQuestionAnswerConnection(
	input: FormQuestionAnswerConnectionInput!,
	first: Int,
	after: String,
	last: Int,
	before: String
): FormQuestionAnswerConnection
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestionAnswer: { rank: 0 } }
    action: "read"
    usesResponse: true
    responseType: "formQuestionAnswer"
  )
```

**Input**

`FormQuestionAnswerConnectionInput`

| Argument       | Type | Description             |
| -------------- | ---- | ----------------------- |
| formId         | ID   | ID of the form          |
| formResponseId | ID   | ID of the form response |
| orgId          | ID   | ID of the org           |

**Query**

```graphql
query GetFormQuestionAnswers($input: FormQuestionAnswerConnectionInput!) {
  formQuestionAnswerConnection(input: $input) {
    nodes {
      id
      formQuestionId
      formResponseId
      value
      metadata
    }
  }
}
```

**Variables**

```graphql
{
  "input": {
    "formId": "6612c7a0-0305-11ed-8f41-738b1c48eaac"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionAnswerConnection": {
      "nodes": [
        {
          "id": "7e686d80-03cf-11ed-9039-70de6585edaf",
          "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
          "formResponseId": "7e65d570-03cf-11ed-9d08-0b3a81ecdcb3",
          "value": "Red",
          "metadata": {
            "something": "useful"
          }
        },
        {
          "id": "173bafc0-03cd-11ed-bf97-0a4671419a57",
          "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
          "formResponseId": "173917b0-03cd-11ed-8edc-6a52fcd0029a",
          "value": "Beef",
          "metadata": {
            "something": "useful"
          }
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

`formQuestionAnswerUpsert`

Creates/updates a form question answer

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestionAnswer: { isAll: true, rank: 0 } }, action: "create")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` requires permission to update the FormQuestionAnswer

```graphql
"""
Creates/updates a form question answer
"""
formQuestionAnswerUpsert(input: FormQuestionAnswerUpsertInput!): FormQuestionAnswerUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestionAnswer: { isAll: true, rank: 0 } }
    action: "create"
  )
```

**Input**

`FormQuestionAnswerUpsertInput`

| Argument       | Type | Description                                     |
| -------------- | ---- | ----------------------------------------------- |
| id             | ID   | ID of the FormQuestionAnswer (if updating)      |
| formQuestionId | ID   | The ID of the FormQuestion                      |
| formResponseId | ID   | The ID of the FormResponse                      |
| value          | JSON | An object containing the answer                 |
| metadata       | JSON | Metadata associated with the FormQuestionAnswer |

**Query**

```graphql
mutation UpsertFormQuestionAnswer($input: FormQuestionAnswerUpsertInput!) {
  formQuestionAnswerUpsert(input: $input) {
    formQuestionAnswer {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "formQuestionId": "be823770-0244-11ed-bbb5-764d11f7aa65",
    "formResponseId": "173917b0-03cd-11ed-8edc-6a52fcd0029a",
    "value": "Chicken",
    "metadata": {
      "something": "useful"
    }
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionAnswerUpsert": {
      "formQuestionAnswer": {
        "id": "5faed3f0-03f4-11ed-ab4a-adf1e6880af7"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formQuestionAnswerBatchUpsert`

Creates/updates a list of form question answers

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

\*`[@hasPermissions*(filters: { formQuestionAnswer: { isAll: true, rank: 0 } }, action: "create")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to update FormQuestionAnswers.

```graphql
"""
Creates/updates a list of form question answers
"""
formQuestionAnswerBatchUpsert(
	input: FormQuestionAnswerBatchUpsertInput!
): FormQuestionAnswerBatchUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { formQuestionAnswer: { isAll: true, rank: 0 } }
    action: "create"
  )
```

**Input**

`FormQuestionAnswerBatchUpsertInput`

| Argument            | Type                                | Description                   |
| ------------------- | ----------------------------------- | ----------------------------- |
| formResponseId      | ID                                  | ID of the form response       |
| formQuestionAnswers | \[FormQuestionAnswerBatchUpsertRow] | List of form question answers |

`FormQuestionAnswerBatchUpsertRow`

| Argument       | Type | Description                                     |
| -------------- | ---- | ----------------------------------------------- |
| id             | ID   | ID of the FormQuestionAnswer (if updating)      |
| formQuestionId | ID   | The ID of the FormQuestion                      |
| value          | JSON | An object containing the answer                 |
| metadata       | JSON | Metadata associated with the FormQuestionAnswer |

**Query**

```graphql
mutation BatchUpsertFormQuestionAnswer(
	$input: FormQuestionAnswerBatchUpsertInput!
) {
  formQuestionAnswerBatchUpsert(input: $input) {
    formQuestionAnswers {
      id
      formQuestionId
      value
      metadata
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "formResponseId": "ecabf7b0-03f4-11ed-b220-1877fc576553",
    "formQuestionAnswers": [
      {
        "formQuestionId": "9ff0f0d0-03f2-11ed-831e-d72cda76aa25",
        "value": "Pasta",
        "metadata": {
          "something": "useful"
        }
      },
      {
        "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
        "value": "Turquoise"
      }
    ]
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionAnswerBatchUpsert": {
      "formQuestionAnswers": [
        {
          "id": "784581e0-03f7-11ed-b574-0316eb266ba9",
          "formQuestionId": "9ff0f0d0-03f2-11ed-831e-d72cda76aa25",
          "value": "Pasta",
          "metadata": {
            "something": "useful"
          }
        },
        {
          "id": "7845d000-03f7-11ed-920a-f5a3c3e47dbf",
          "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
          "value": "Turquoise",
          "metadata": null
        }
      ]
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formQuestionAnswerDeleteById`

Deletes a form question answer

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formQuestionAnswer: { idArg: "id", rank: 0 } }, action: "delete")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to update the FormQuestionAnswer

```graphql
"""
Deletes a form question answer
"""
formQuestionAnswerDeleteById(
	input: FormQuestionAnswerDeleteByIdInput!
): FormQuestionAnswerDeleteByIdPayload
  @authOrApiAuth 
  @hasPermissions(filters: { formQuestionAnswer: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`FormQuestionAnswerDeleteByIdInput!`

| Argument | Type | Description                    |
| -------- | ---- | ------------------------------ |
| id       | ID   | ID of the form question answer |

**Query**

```graphql
mutation DeleteFormQuestionAnswer($input: FormQuestionAnswerDeleteByIdInput!) {
  formQuestionAnswerDeleteById(input: $input) {
    formQuestionAnswer {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "id": "7e686d80-03cf-11ed-9039-70de6585edaf"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formQuestionAnswerDeleteById": {
      "formQuestionAnswer": {
        "id": "7e686d80-03cf-11ed-9039-70de6585edaf"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

