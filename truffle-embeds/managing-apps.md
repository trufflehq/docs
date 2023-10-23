---
description: Use truffle-cli to manage your apps.
---

# Managing Apps

If you haven't already, make sure that you are signed in with

```bash
truffle-cli login
```

Then set an org to work in

```bash
truffle-cli org use <org-slug-or-id>
```

To check which user and org you're using, use `truffle-cli whoami`.

```
Using API: https://mothertree.truffle.vip/graphql
You are signed in as 'Dev'
Email: dev@truffle.vip
User ID: ccca0e50-80ea-11ed-8427-2ce2ffa58b3c

You are using org 'Truffle'
Slug: truffle
Org ID: c803bc70-6bdb-11eb-a8c3-3441a1187d5e
```

Now go to your project directory (wherever you have the rest of your code), and create a new truffle app inside that directory with

```bash
truffle-cli app create <app-slug>
```

This will write a `truffle.config.mjs` file to the current directory. You can modify it to add your embeds.

```javascript
export default {
  path: '@truffle/my-first-app',
  name: 'My First Truffle App',
  embeds: [
    {
      slug: 'my-first-embed',
      url: 'https://my-truffle-app.netlify.app/',
      contentPageType: 'youtubeLive'
    }
  ]
};
```

{% hint style="info" %}
You can learn more about embed options [here](../reference/embed-config.md).
{% endhint %}

When you're done writing your truffle app config, deploy it with

```bash
truffle-cli app deploy
```

{% hint style="info" %}
If you ever need to retrieve your deployed config, `run truffle-cli app clone <app-path>`. In this example, it would be `truffle-cli app clone @truffle/my-first-app`.
{% endhint %}

Then install it in your org with

```bash
truffle-cli app install @truffle/my-first-app
```

Congrats! You've created your first production truffle app, deployed it, and installed it into your org! The embeds you defined in your config should appear on the live stream on your linked channel.

