# Deploying an Embed on Youtube or Twitch

In the last tutorial, I showed you how to create a basic Truffle embed and test it inside of the [Embed Dev Viewer](https://app.truffle.vip/dev/embed). In this tutorial, I'll show you how to get it to appear as a Windowed Embed on a Youtube or Twitch livestream.

Before we get started make sure you have the [Truffle Browser Extension](https://truffle.vip/extension) installed.

In order to get our embed to show up on our livestream, we're going to need to link our Youtube or Twitch account to our Truffle org. To do this, head over to [https://app.truffle.vip/creator](https://app.truffle.vip/creator) and select your org. Then select "Settings" in the left pane. You'll be given the opportunity to link your Youtube or Twitch account.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Channel link page in app.truffle.vip</p></figcaption></figure>

If you're using Youtube, it's helpful to set up a "Test Stream" to test your embeds on. Do so by creating a scheduled stream in Youtube Studio.&#x20;

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Creating a scheduled stream in Youtube Studio</p></figcaption></figure>

Now let's go back to our `truffle.config.mjs` file. We'll add an array with one embed.&#x20;

```javascript
export default {
  path: "@my-org/my-truffle-app",
  name: "sparks-test-1",
  cliVersion: "0.6.1",
  embeds: [
    {
      slug: "my-embed",
      url: "http://localhost:5173",
      contentPageType: "youtubeLive",
      iconUrl: "https://cdn.bio/assets/icons/global/light/add_on.svg",
      windowProps: {
        title: "My First Embed",
      },
    },
  ],
};
```

The most important prop in the embed config is the `url` prop. This tells the extension which web page should get rendered. When you deploy your web app to the hosting provider of your choice, change the `url` prop to the url of your production site.

{% hint style="info" %}
For more details about the embed config, take a look [here](../reference/embed-config.md).
{% endhint %}

Now if you visit your test stream, you should see your new embed by selecting it from the side bar.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Our first deployed windowed embed</p></figcaption></figure>

Congrats! You have successfully added an embed to your own stream page!
