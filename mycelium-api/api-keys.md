# API Keys

If you're developing a site or a component, you won't need an API key since our browser client library handles authentication for you. Learn more about that on the [Interacting with Mycelium](../front-end-dev/interacting-with-our-backend.md) page in the front-end dev section.

If you're writing code somewhere else (i.e. a server, serverless function, or raspberry pie), you're in the right place!

There are two types of API keys: org keys and package keys. You'll usually use org keys to authenticate truffle-cli. Package keys will be the ones that you set in the env for your server.

## Org keys

### Obtaining org keys

Currently, we have no good way for you to get your own org key :sweat\_smile:. Just shoot us a message and we'll get one for you.

### Using org keys

When you use an org key, you are performing actions as if you were the administrator of that org. You can install/uninstall packages, create packages, manage org users, and mutate objects (such as collectibles) all without restriction. For this reason, you must be _very careful_ as to where you store your org key.

#### truffle-cli

You can use an org key to authenticate `truffle-cli`. To do so, simply invoke

```bash
truffle-cli auth <org_key>
```

This will set the global configuration at `~/.truffle/config.json`.

#### HTTP

To use an org key in a HTTP request, pass it as a bearer token via the `Authorization` header (e.g. `Authorization: Bearer <org_key>`). Mycelium will be able to determine which org it is from the key and uses that information to contextualize many of the queries and mutations you make. For example, the following query will return the org slug and name associated with the key without explicitly having to specify the org id:

```graphql
query {
  org {
    slug
    name
  }
}
```

Full cURL command:

```bash
curl --location --request POST 'https://mycelium.staging.bio/graphql' \
--header 'Authorization: Bearer <org_key>' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"query { org { slug name } }","variables":{}}'
```

Response:

```json
{
  "data": {
    "org": {
      "slug": "dev",
      "name": "Buildooooooors and Shipooors"
    }
  },
  "extensions": {
    "components": {}
  }
}
```

## Package keys

### Obtaining package keys

When you invoke

```bash
truffle-cli create <package_name>
```

or

```bash
truffle-cli fork <source_package> <new_package>
```

truffle-cli will retrieve a package key and save it in `truffle.secret.mjs`. If you lose your package key, you can cd into your package's directory and invoke

```bash
truffle-cli regenerate-api-key
```

to generate a new package key.

### Using package keys

When you use a package key, you are performing actions as a third party with limited access to an org. When a creator installs your package on their org, they grant your package permission to access the resources defined in the `requestedPermissions` array inside of your `truffle.config.mjs` file.

{% hint style="warning" %}
If you try to access an org that hasn't installed your package using your package API key, Mycelium will throw an error.
{% endhint %}

#### HTTP

To use a package key in a HTTP request, pass it as a bearer token via the `Authorization` header (e.g. `Authorization: Bearer <org_key>`). You must also pass the id of the org you are interacting with via the `x-org-id` header for Mycelium to contextualize your query.&#x20;

Example cURL command:

```bash
curl --location --request POST 'https://mycelium.staging.bio/graphql' \
--header 'x-org-id: <org_id>' \
--header 'Authorization: Bearer <package_key>' \
--header 'Content-Type: application/json' \
--data-raw '{"query":"query { org { slug name } }","variables":{}}'
```

Response:&#x20;

```json
{
  "data": {
    "org": {
      "slug": "dev",
      "name": "Buildooooooors and Shipooors"
    }
  },
  "extensions": {
    "components": {}
  }
}
```
