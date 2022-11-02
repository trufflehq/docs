---
description: Truffle Functions is Truffle's bespoke serverless function ecosystem.
---

# Introduction

Truffle Functions execute TypeScript code in the Deno Runtime. Creating a new function is quick and easy.

### Creating your first Function

In your existing `truffle.config.mjs` file, add the definition for your Function:

{% hint style="danger" %}
Due to the nature of DNS, function slugs are case insensitive, and every one is unique.\
`render` and `calculatesum` have been reserved by Truffle for documentation purposes.
{% endhint %}

```diff
export default {
  name: "@early-access-carter/optic",
  version: "0.0.1",
  apiUrl: "http://mycelium.staging.bio/graphql",
  requestedPermissions: [
    {
      filters: {
        edgeFunction: { isAll: true, rank: 0 },
      },
      action: "update",
      value: true,
    }
    {
      filters: {
        edgeDeployment: { isAll: true, rank: 0 },
      },
      action: "update",
      value: true,
    },
  ],
  installActionRel: {},
+ functions: [
+  {
+    slug: 'calculatesum',
+    description: 'Calculates the sum of multiple numbers',
+    entrypoint: './src/sum.ts'
+   }
+ ]
}
```

{% hint style="warning" %}
From this point, make sure you do a `truffle-cli deploy` to make sure that all of the permissions are set up.
{% endhint %}

Then, create the `sum.ts` file and create a web server:

```typescript
import { serve } from "https://deno.land/std@0.149.0/http/server.ts";

serve(
  (req) => {
    const url = new URL(req.url);
    console.dir(url);
    const xs = url.searchParams.getAll("x").map(Number);
    console.log(new Date().toISOString(), req.method, url.pathname)

    return new Response(
      JSON.stringify({
        sum: xs.reduce((a, b) => (a += b), 0),
        xs,
      }),
      {
        headers: {
          "Content-Type": "application/json",
        },
      }
    );
  },
  {
    onListen({ port, hostname }) {
      console.log(`Server started at http://${hostname}:${port}`);
    },
  }
);
```

Now, you're ready to deploy your function! It's as simple as running:

```bash
truffle-cli functions deploy calculatesum
```

And that's it! Your function is now deployed to the Truffle Functions registry and is ready to start being executed.

### Using JSX

With the Deno runtime, you can directly run TSX files! Let's take advantage of that to make a super smol React app. Start by updating your `truffle.config.mjs` again:

```diff
export default {
  name: "@early-access-carter/optic",
  version: "0.0.1",
  apiUrl: "http://mycelium.staging.bio/graphql",
  requestedPermissions: [
    {
      filters: {
        edgeFunction: { isAll: true, rank: 0 },
      },
      action: "update",
      value: true,
    },
    {
      filters: {
        edgeDeployment: { isAll: true, rank: 0 },
      },
      action: "update",
      value: true,
    }
  ],
  installActionRel: {},
  functions: [
   {
     slug: 'calculatesum',
     description: 'Calculates the sum of multiple numbers',
     entrypoint: './src/sum.ts'
-  }
+  },
+  {
+    slug: 'render',
+   description: 'Renders JSX',
+   entrypoint: './src/index.tsx'
+  }
  ]
}
```

Then create the `./src/index.tsx` file:

```tsx
// index.tsx
/** @jsx h */
import { serve } from "https://deno.land/std@0.114.0/http/server.ts";
import { h, ssr, tw } from "https://crux.land/nanossr@0.0.1";

const Hello = (props: { name: string }) => (
  <div class={tw`bg-white flex h-screen`}>
    <h1 class={tw`text-5xl text-gray-600 m-auto mt-20`}>
      Hello {props.name}!

      The time is {new Date().toLocaleString()}
    </h1>
  </div>
);

console.log("Listening on http://localhost:8000");
serve((req) => {
  const url = new URL(req.url);
  const name = url.searchParams.get("name") ?? "world";
  return ssr(() => <Hello name={name} />);
});
```

I think you're getting the hang of it. Now, you can deploy your function!

```
truffle-cli functions deploy render
```

### Accessing your Functions

You can access your current production deployment at `https://{FUNCTION_SLUG}.edge.truffle.vip`.

To access a specific deployment ID, use `https://{FUNCTION_SLUG}-{DEPLOYMENT_ID}.edge.truffle.vip`.
