---
description: >-
  Represents a single response to a form. A FormResponse acts a collection of
  FormQuestionAnswers
---

# FormResponse

### Resolvers

`formResponse`

Returns a FormResponse

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formResponse: { idArg: "id", rank: 0 } }, action: "read", modelUserIdKey: "userId", usesResponse: true, responseType: "formResponse")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

requires permissions to read the FormResponse

```graphql
"""
Returns a FormResponse
"""
formResponse(input: FormResponseInput!): FormResponse
  @authOrApiAuth
  @hasPermissions(
    filters: { formResponse: { idArg: "id", rank: 0 } }
    action: "read"
    modelUserIdKey: "userId"
    usesResponse: true
    responseType: "formResponse"
  )
```

**Input**

`FormResponseInput`

| Argument | Type | Description             |
| -------- | ---- | ----------------------- |
| id       | ID   | ID of the form response |

**Query**

```graphql
query GetFormResponse($input: FormResponseInput!) {
  formResponse(input: $input) {
    id
    orgId
    formId
    userId
    metadata
    time
    formQuestionAnswerConnection {
      nodes {
        id
        formQuestionId
        value
      }
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "id": "173917b0-03cd-11ed-8edc-6a52fcd0029a"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formResponse": {
      "id": "173917b0-03cd-11ed-8edc-6a52fcd0029a",
      "orgId": "e2853b00-0243-11ed-bf99-3b2dd8713144",
      "formId": "6612c7a0-0305-11ed-8f41-738b1c48eaac",
      "userId": "3b436b30-0240-11ed-b1e6-09d9961b4f27",
      "metadata": {
        "something": "useful"
      },
      "time": "2022-07-14T23:31:31.115Z",
      "formQuestionAnswerConnection": {
        "nodes": [
          {
            "id": "173bd6d0-03cd-11ed-a334-9e29c2d5a232",
            "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
            "value": "Red"
          },
          {
            "id": "173bafc0-03cd-11ed-bf97-0a4671419a57",
            "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
            "value": "Beef"
          }
        ]
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formResponseConnection`

Returns a paginated list of FormResponses

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formResponse: { rank: 0 } }, action: "read", modelUserIdKey: "userId", usesResponse: true, responseType: "formResponse")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)`

```graphql
formResponseConnection(
	input: FormResponseConnectionInput!,
	first: Int,
	after: String,
	last: Int,
	before: String
): FormResponseConnection
    @authOrApiAuth
    @hasPermissions(
      filters: { formResponse: { rank: 0 } }
      action: "read"
      modelUserIdKey: "userId"
      usesResponse: true
      responseType: "formResponse"
    )
```

**Input**

`FormResponseConnectionInput`

| Argument | Type    | Description                                                                                                               |
| -------- | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| formId   | ID      | ID of the form                                                                                                            |
| orgId    | ID      | ID of the org                                                                                                             |
| isMe     | Boolean | Flag for whether you want to return responses for the auth'd user                                                         |
| userId   | ID      | ID of the user                                                                                                            |
| minTime  | String  | Exclude responses earlier than minTime. Specify using ISO 8601 format (the format used by Javascript Date.toISOString()). |
| maxTime  | String  | Exclude responses later than maxTime. Specify using ISO 8601 format (the format used by Javascript Date.toISOString()).   |

**Query**

```graphql
query FormResponseConnection($input: FormResponseConnectionInput!) {
  formResponseConnection(input: $input) {
    nodes {
      id
      userId
      time
      formQuestionAnswerConnection {
        nodes {
          formQuestionId
          value
        }
      }
    }
  }
}
```

**Variables**

```json
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
    "formResponseConnection": {
      "nodes": [
        {
          "id": "173917b0-03cd-11ed-8edc-6a52fcd0029a",
          "userId": "3b436b30-0240-11ed-b1e6-09d9961b4f27",
          "time": "2022-07-14T23:31:31.115Z",
          "formQuestionAnswerConnection": {
            "nodes": [
              {
                "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
                "value": "Red"
              },
              {
                "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
                "value": "Beef"
              }
            ]
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

`formResponseUpsert`

Create or update a form response

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formResponse: { isAll: true, rank: 0 } }, action: "create")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have permission to write to the form response

```graphql
"""
Create or update a form response
"""
formResponseUpsert(input: FormResponseUpsertInput): FormResponseUpsertPayload
  @authOrApiAuth
  @hasPermissions(
    filters: { formResponse: { isAll: true, rank: 0 } }
    action: "create"
  )
```

**Input**

`FormResponseUpsertInput`

| Argument            | Type                                | Description                                |
| ------------------- | ----------------------------------- | ------------------------------------------ |
| id                  | ID                                  | ID of the form response                    |
| formId              | ID                                  | ID of the form                             |
| formQuestionAnswers | \[FormQuestionAnswerBatchUpsertRow] | Answers to the form questions              |
| metadata            | JSON                                | Metadata associated with the form response |

**Query**

```graphql
mutation ($input: FormResponseUpsertInput) {
  formResponseUpsert(input: $input) {
    formResponse {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "formId": "6612c7a0-0305-11ed-8f41-738b1c48eaac",
    "formQuestionAnswers": [
      {
        "formQuestionId": "f78dcaf0-03cc-11ed-a594-f148c9ab48c3",
        "value": "Beef"
      },
      {
        "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
        "value": "Red"
      }
    ],
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
    "formResponseUpsert": {
      "formResponse": {
        "id": "7e65d570-03cf-11ed-9d08-0b3a81ecdcb3"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```



`formResponseDeleteById`

Delete a form response

**Directives**

`[@authOrApiAuth](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` can read with authenticated user or valid api key

`[@hasPermissions(filters: { formResponse: { idArg: "id", rank: 0 } }, action: "delete")](../GraphQL%20API%20207272de93e94ddfb1c2ba16934af72f.md)` must have write access to the form response

```graphql
"""
Delete a form response
"""
formResponseDeleteById(input: FormResponseDeleteByIdInput!): FormResponseDeleteByIdPayload
  @authOrApiAuth
  @hasPermissions(filters: { formResponse: { idArg: "id", rank: 0 } }, action: "delete")
```

**Input**

`FormResponseDeleteByIdInput`

| Argument | Type | Description                       |
| -------- | ---- | --------------------------------- |
| id       | ID   | ID of the form response to delete |

**Query**

```graphql
mutation DeleteFormResponse($input: FormResponseDeleteByIdInput!) {
  formResponseDeleteById(input: $input) {
    formResponse {
      id
    }
  }
}
```

**Variables**

```json
{
  "input": {
    "id": "7e65d570-03cf-11ed-9d08-0b3a81ecdcb3"
  }
}
```

**Sample Response**

```json
{
  "data": {
    "formResponseDeleteById": {
      "formResponse": {
        "id": "7e65d570-03cf-11ed-9d08-0b3a81ecdcb3"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

