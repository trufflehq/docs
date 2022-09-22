# Getting started with forms

## Introduction

Forms are a powerful way to collect information directly from users. In this tutorial, you will

* Create a form
* Craft mutations that your users will use to respond to the form
* Query responses from individual users

## Creating a form

Creating a form is easy. Simply specify a name and the id of the org that you want to create the form for.

```graphql
mutation {
  formUpsert(input: {
    name: "My first form",
    orgId: "MY_ORG_ID"
  }) {
   form {
     id
     name
   } 
  }
}
```

The response should look something like this:

```json
{
  "data": {
    "formUpsert": {
      "form": {
        "id": "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
        "name": "My first form"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

Now that we have a form, we’re going to want some questions to go with it. Let’s insert one. To specify that this question belongs to the form we created, we pass the id of the form we created in the previous step.

```graphql
mutation {
  formQuestionUpsert(input: {
    formId: "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
    question: "What is your favorite food?"
  }) {
    formQuestion {
      id
			question
    }
  }
}
```

Response:

```json
{
  "data": {
    "formQuestionUpsert": {
      "formQuestion": {
        "id": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
				"question": "What is your favorite food?"
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

Great! You’ve created a form with a question! Now let’s move on to the next part where we will craft mutations that your users will use to respond to your form.

## Responding to a form

When you’re building the UI for your users to respond to the form, you’ll probably want all the information about the form and its questions to display to the user. We can query a form and its questions like so:

```graphql
query {
  form(input: {
		id: "2193a280-02f5-11ed-9a0c-260e1a9a0ae5"
	}) {
    id
    name
    formQuestionConnection {
      nodes {
        id
        question
      }
    }
  }
}
```

This will generate a response that looks like this:

```json
{
  "data": {
    "form": {
      "id": "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
      "name": "My first form",
      "formQuestionConnection": {
        "nodes": [
          {
            "id": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
            "question": "What is your favorite food?"
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

Once your user fills out your form, they’ll click some kind of submit button that invokes a mutation to record their response. Here’s what that mutation would look like:

```graphql
mutation($questionsAnswers: JSON!) {
	formResponseUpsert(input: {
    formId: "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
    formQuestionAnswers: $questionsAnswers
  }) {
    formResponse {
      id
    }
  }
}
```

Then you can pass the user’s responses to questions via GraphQL variables:

```graphql
{
  "questionsAnswers": [
    {
      "formQuestionId": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
      "value": "Beef"
    }
  ]
}
```

Congrats! You’ve built a mechanism for your users to submit responses. Now let’s see what your users have to say!

## Querying responses

After you’ve given your users a chance to respond to your form, you’ll want to see how they responded. This query will get the first 10 responses to your form:

```graphql
query {
  form(input: {
		id: "2193a280-02f5-11ed-9a0c-260e1a9a0ae5"
	}) {
    id
    name
    formQuestionConnection  {
      nodes {
        id
        question
      }
    }
    formResponseConnection(first: 10) {
      nodes {
        id
        formQuestionAnswerConnection {
          nodes {
            id
            value
          }
        }
      }
    }
  }
}
```

Here’s the response:

```json
{
  "data": {
    "form": {
      "id": "2193a280-02f5-11ed-9a0c-260e1a9a0ae5",
      "name": "My first form",
      "formQuestionConnection": {
        "nodes": [
          {
            "id": "517dd000-02fb-11ed-929d-5b59cc41d708",
            "question": "What is your favorite color?"
          },
          {
            "id": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
            "question": "What is your favorite food?"
          }
        ]
      },
      "formResponseConnection": {
        "nodes": [
          {
            "formQuestionAnswerConnection": {
              "nodes": [
                {
                  "formQuestionId": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
                  "value": "Beef"
                },
                {
                  "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
                  "value": "Red"
                }
              ]
            }
          },
          {
            "formQuestionAnswerConnection": {
              "nodes": [
                {
                  "formQuestionId": "b0c62200-02e3-11ed-9a09-e87a8e7384eb",
                  "value": "Chicken"
                },
                {
                  "formQuestionId": "517dd000-02fb-11ed-929d-5b59cc41d708",
                  "value": "Blue"
                }
              ]
            }
          },
					...
        ]
      }
    }
  },
  "extensions": {
    "components": {}
  }
}
```

Congrats! You’ve reached the end of the tutorial. Now go make some forms!
