---
description: >-
  Mycelium powers all of Truffle's back end features. It exposes a GraphQL API
  so that you can use it in your packages!
---

# Introduction

Mycelium is the brain of this operation we call Truffle. It manages all the information for orgs, users, and packages. We interact with it using a GraphQL API. If you haven't used GraphQL before, I'll tell you right now, it's pretty cool. You can learn more about it on the [official website](https://graphql.org/).

If you're developing a site or a component, you can use our client library to interact with it. The client library handles all of the initialization and authentication automatically, so it's super easy to get started. You can learn more about that by reading the docs on [Interacting with Mycelium](../front-end-dev/interacting-with-our-backend.md) in the front-end dev section.

If you're writing code elsewhere (i.e. a serverless function, your own server, or maybe a raspberry pi), you'll need to authenticate using an API key. You can learn more about that by reading the docs on [API Keys](api-keys.md).

To prevent mischievous users from doing mischievous things, we have a robust permissions system. Learn more about that by reading the docs on [Permissions](broken-reference).

### API explorer

If you have an API key and you're ready to start playing around with the API, head over to our [API Explorer](https://staging.bio/org/truffle-dev-early-access/api-explorer). There you can view the API docs and execute queries.
