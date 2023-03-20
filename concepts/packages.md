---
description: Packages are what makes Truffle useful! Read on to learn about how they work.
---

# Packages

## Disclaimer: Some of this information may be outdated

## Overview

At the most basic level, a package is simply a container that implements a feature or collection of features that a creator can use with their Org. You can think of them like an npm package. Packages create features by

* Creating a **site** that users can log into with their Truffle account and interact with.
* Providing **UI components** that a creator or other packages can use.
* Providing **open-source, hosted, versioned code** that the package can use, or other packages can use.
* Providing **embeds** that can be used inside of the truffle.tv browser extension.
* Interacting with the truffle's **Mycelium API**.
* Creating **actions** that can be triggered by core Truffle platform features or other packages.
* Creating and subscribing to **event topics** generated **** from the Truffle platform or other packages.&#x20;

### Creating sites

Each package has its own site that is rendered through web components. This allows developers to create sites using whatever framework supports web component creation including React, Vue, and Svelte.

When you invoke `truffle-cli create` on the command line, it will fork the default package and give you some code to get started with creating a site. Check out the docs on [Creating a site](../front-end-dev/how-packages-are-used.md) to learn more.

### Providing UI components for creators

By following our spec (yet to be defined, but involves creating a web component and registering props), you can create components that creators can easily embed into their existing Truffle sites using the site builder.

### Providing code for other packages

Here at Truffle, we believe that web components, ESM modules, and URL based imports are the future of JavaScript. That's why we chose Deno for the runtime of our back end rendering engine. When you deploy a package to Truffle, all of the files in the package are hosted on tfl.dev, so anyone can view and use the source code.

Let's say someone that has the org "coolorg" deploys a package called "cool-components" at version 1.0.0 with the following component:

{% code title="/components/hello-world.ts" %}
```jsx
import React from 'https://npm.tfl.dev'
import { toDist } from 'https://tfl.dev/@truffle/distribute@^2.0.0/format/wc/react/index.ts'

function HelloWorld () {
    return <h1>Hello world</h1>
}

export const Component = toDist(HelloWorld, import.meta.url);
export const HelloWorldWebComponent = Component.tagName
```
{% endcode %}

Another package developer could use that component simply by importing it:

{% code title="/routes/page.tsx" %}
```tsx
import React from 'https://npm.tfl.dev'
import { toDist } from 'https://tfl.dev/@truffle/distribute@^2.0.0/format/wc/react/index.ts'

// import a component from another package
import { HelloWorldWebComponent } from 'https://tfl.dev/@coolorg/cool-components@^1.0.0/components/hello-world.ts'

function MyPage () {
    return (
        <>
            ... some other content
            <HelloWorldWebComponent />
            ... some other content
        </>
    )
}

export default toDist(MyPage, import.meta.url)
```
{% endcode %}

{% hint style="info" %}
Notice that in both files we import React from npm.tfl.dev. Standard Node libraries are hosted on npm.tfl.dev while Truffle package files are hosted on tfl.dev.
{% endhint %}

### Providing a truffle.tv embed

If you're a fan of Ludwig, DrLupo, LilyPichu, or Myth, and you have the truffle.tv browser extension installed, you've probably seen this interface:

![A screenshot of the mogul-menu truffle.tv embed](<../.gitbook/assets/image (1) (2).png>)

The screenshot above is of our own mogul-menu embed, but any package developer has the power to create one! Using truffle.tv embeds, you can easily add features to YouTube or Twitch. To learn more, you can read the docs on [truffle.tv embeds](broken-reference)

### Creating actions

Actions provide a way for other parts of the Truffle ecosystem to hook into your package and 3rd party services that may be supporting your package. There are four types of actions:

1. GraphQL actions allow you to define a query to be executed against the Mycelium API.
2. Webhook actions allow you to send a request to a remote endpoint.
3. Google PubSub actions allow you to notify a Google PubSub topic.
4. Workflow actions allow you to execute a sequence of other actions.

To trigger an action, you'll use a reference to it that will look like `@coolorg/coolpackage@latest/_Action/coolaction`. To learn more about actions, you can read the docs on [Actions](broken-reference).

### Creating and subscribing to event topics

Here at Truffle, we understand that things happen. That's why we created event topics. An event topic represents some type of event that can occur from a core Truffle feature or a feature implemented by a package.

As an example, let's say we were building a package that featured an integration with a particular Minecraft server. On Truffle, users would have the ability to acquire collectibles and redeem them for in-game items. One of these collectibles might look like this:

```json
{
    "id": "812e886e-0d3a-11ed-860c-7fe5a81882f6",
    "name": "Diamonds",
    "type": "redeemable",
    "data": {
        "redeemType": "event",
        "redeemData": {
            "eventTopicSlug": "minecraft-item-redeem-topic"
        }
    }
}
```

In the snippet above, notice how the collectible has `redeemType` set to `event` and has also defined an `eventTopicSlug`. This instructs the Mycelium API to notify the `minecraft-item-redeem-topic` whenever a user redeems the Diamonds collectible.

Inside your package, you can create a subscription to the `minecraft-item-redeem-topic`. Subscriptions of topics will execute an action whenever that topic gets notified of an event. In this case, we want to trigger a webook that hits an endpoint exposed by our Minecraft server. The subscription might look like this:

```json
{
    "id": "1f2159e2-0d3c-11ed-be57-13b87ea70f95",
    "eventTopicPath": "@coolorg/coolpackage@latest/_EventTopic/minecraft-item-redeem-topic",
    "actionRel": {
        "actionPath": "@truffle/core@latest/_Action/webhook",
        "runtimeData": {
            "endpoint": "https://minecraft.coolserver.net"
        }
    }
}
```

In the snippet above, `eventTopicPath` specifies which topic the subscription is listening to, and the `actionRel` specifies which action is going to get executed when the topic receives an event. We also provide `runtimeData` that lets us customize the behavior of specific actions. In this case, we specify `endpoint` for the webhook action. To learn more, you can read the docs on [Events](broken-reference).

## Going further

Hopefully this page gave you a good overview of what a Package is and how you can use them to build custom features for creators. If you have an idea for a package but aren't sure how to implement it, it might be helpful to click one of the links on this page to learn more about a particular aspect of the Truffle platform. If you're just starting out or just want to explore, consider trying one of the tutorials.&#x20;
