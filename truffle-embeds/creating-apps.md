---
description: Creating Your First Truffle App
---

# Creating Apps

{% embed url="https://youtu.be/6umrC-oLpow" %}



At this point you should have a basic web app running in localhost or online, the Truffle Extension, and the Truffle CLI. Instructions for installing everything are here: [getting-started.md](getting-started.md "mention")

## Putting your web app into an embed

Go to any YouTube video or stream and open up the dev tools by right-clicking and clicking "inspect", or by hitting the `F12` key on your keyboard.

If you have the Truffle browser extension installed you should see an option for the Truffle dev tools!

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The Truffle dev tools let you easily add and delete embeds!

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

In the Embed Config table, change http://localhost:8080 to the localhost url of your own application, and then click "Add."

This embed config is documented here: [embed-config.md](../reference/embed-config.md "mention")

\
This will allow you to test the embed, but getting user info will not work if you don't fill in the Auth token (lets worry about this in [truffle-data-in-apps.md](truffle-data-in-apps.md "mention"))

Refresh the page and you should see your shiny new embed show up below the video's description!

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Congrats! You've created your first embed. But that's not all... we have more to offer you.

## Manipulating the Embed

If you simply want to embed a static page into a YouTube video or live stream page, then following the above instructions may be enough for you. If you want to go one step further, you can use the **Truffle JavaScript SDK** to dynamically control the appearance of the embed from within your site.

### Examples

If you're ready to jump in and read some code, check out our [examples](https://github.com/trufflehq/truffle-packages/tree/0b7189daa625ac339e872fea19020ee26eb1c266/npm/sdk/examples).

### Installing the SDK

If you're using a frontend framework like [React](../reference/mycelium-api/models/economyaction/) or [Vue](https://vuejs.org/), you can simply run npm install.

```shell
npm install @trufflehq/sdk
```

Or if you're a yarn user

```shell
yarn add @trufflehq/sdk
```

Then import the embed object like so:

```javascript
import { getEmbed } from '@trufflehq/sdk'
```

If you're not using a framework or a module bundler, you can simply import it as a module directly in a script.

```html
<script type="module">
   import { getEmbed } from 'https://npm.tfl.dev/@trufflehq/sdk'
   
   // ...
</script>
```

### Using the SDK

Now that you have the SDK imported, you can call `getEmbed()` and manipulate the embed.

```javascript
const embed = getEmbed();
```

You can set the size using css units.

```javascript
embed.setSize("500px", "500px")
```

You can set the position (also using css units).

```javascript
embed.setPosition("25%", "25%")
```

You can also set the visibility.

```javascript
embed.hide()
embed.show()
embed.setVisibility(true)
```

If none of those methods satisfy your needs, you can set custom css styles on the iframe.

```javascript
embed.setStyles({
  border: "5px solid red"
})
```

You can also clear the styles on the iframe.

```javascript
embed.resetStyles()
```

With that, you should have enough flexibility to build some pretty cool shit with the Truffle browser extension!
