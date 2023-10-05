---
description: An brief introduction to Truffle and Truffle apps
---

# What Are Truffle Apps?

**Introduction**

Welcome to the Truffle Developer Platform docs! If you are looking at these docs, you probably want an easy cross-platform way to create interactive experiences for creators and their viewers.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>Snuffle the pig hacking into the mainframe</p></figcaption></figure>

**What is Truffle?**

Truffle is the company behind the Truffle browser extension. Our extension, originally Mogul.TV (built by Otto) was built for Ludwig to help make YouTube better for livestreamers. Since then, the Truffle team has taken over, and we have supercharged the extension so that 3rd party developers like you can build a killer app and deploy to any streamer on any platform.

**What is a Truffle App?**

Truffle apps are web apps that get iframed and displayed to the end users. You choose your favorite frontend framework and your own backend, then build a web app that talks to the Truffle browser extension through the Truffle SDK.&#x20;

**Which platforms does Truffle support?**

Truffle currently only supports Twitch and YouTube for 3rd party apps. We're exploring expansions to other platforms like Kick or any other site, based on community interest (so reach out if you are interested).

The Truffle browser extension is currently only supported on Firefox and Chromium based browsers.

**How Can End Users Interact with My App?**

Truffle apps can consist of one or more embeds, depending on how you want your app to interface with the viewers, mods, or streamers.

* **Windowed Embeds**: Shown as icons in the Truffle sidebar and offer a less intrusive experience. Users can click on the icon to pop open a draggable iFrame window with your app content.
* **Page Embeds**: Directly injected onto the Twitch or YouTube page, allowing for a more integrated experience with the video or stream.
* **Quick Action Embeds:** Streamers can interact with Truffle apps using the Quick Action Interface, which you should hook up to trigger events for viewers like starting a prediction.

**Choosing a Development Framework**

While the Truffle SDK does support most web development frameworks ask for support in our discord if something breaks), we recommend using Vite and React, if you aren't sure what to choose as most of our tutorials will use that for the tech stack.



Follow our getting started guide to build your first App!

{% content-ref url="truffle-embeds/getting-started.md" %}
[getting-started.md](truffle-embeds/getting-started.md)
{% endcontent-ref %}

##







\
