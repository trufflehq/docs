# Truffle.TV Embeds

"Embeds" are how you can add functionality to creators' content through [the browser extension.](https://chrome.google.com/webstore/detail/mogultv/bkkjeefjfjcfdfifddmkdmcpmaakmelp)

#### Quick extension overview

The core of the extension itself is fairly lightweight. It serves two main purposes:

1.  Adding iframes/widgets to a page (we call them "Embeds")

    eg. Adding a menu for channel points and predictions to a YouTube stream
2.  A mutation observer and light modification/styling of DOM elements in a page

    eg. Observing new chat messages and replacing strings in the message body with emotes

#### Setting up your first embed

{% embed url="https://youtu.be/zGLuD8knFro" %}

#### Testing

First, visit test stream: [https://www.youtube.com/watch?v=Xe5KJINZGRA](https://www.youtube.com/watch?v=Xe5KJINZGRA)

Then open Chrome dev tools console and run

```javascript
localStorage.setItem(
  'truffle:devExtensionMappings', 
  JSON.stringify([{
    "id": "localhost",
    "defaultLayoutConfigSteps": [
      { "action": "querySelector", "value": "body" },
      { "action": "appendSubject" }
    ],
    "domAction": "append",
    "iframeUrl": "http://localhost:8000/embed", // change this to your route
    "orgId": "8e35b570-6c2f-11ec-bade-b32a8d305590",
    "slug": "anything"
  }])
)
```

This will tell the browser extension to add your Embed into any page on youtube.com

{% hint style="warning" %}
Using http://localhost:8000 as your Embed url will only work if Chrome is launched in insecure mode:

**Linux**: `google-chrome --allow-running-insecure-content`\
**Mac:** `/Applications/Google\\ Chrome.app/Contents/MacOS/Google\\ Chrome --allow-running-insecure-content </dev/null &>/dev/null &`

If you don't want to use insecure mode, you can deploy and use the hosted site, eg:&#x20;

`https://<packageVersionId>.sporocarp.dev/embed`
{% endhint %}

### More than just an iframe

Embeds need to do more than just exist as a static iframe on the page; they need to be able to modify the current page, and their own iframe styles.

Jumper is a library we use to communicate between your iframed package and the parent page (YouTube, Twitch, etc...).

#### Jumper calls

#### `layout.applyLayoutConfigSteps`

This lets you change DOM styles, replace text with images, etc… in the parent page (eg YouTube)

```jsx
useEffect(() => {
    const style = {
      background: "#ff0000"
    };
    // sets the iframe background color to red
    jumper.call("layout.applyLayoutConfigSteps", {
      layoutConfigSteps: [
        { action: "useSubject" }, // start with our iframe
        { action: "setStyle", value: style },
      ],
    });
  }, []);
```

In the following, **element** refers to the DOM element the styles are being applied to, and **subject** refers to what these configSteps are applying _with_. eg appendSubject appends _to_ **element**, _with_ **subject.**

Element always starts as `document.documentElement` and subject always starts as the iframe holding the embed

Available configSteps

* `appendSubject`
* `useDocument`
  * Sets the element to `document`
* `useSubject`
  * Sets the element to be the current subject
* `insertSubjectBefore`
* `insertSubjectAfter`
* `querySelector`
  * Runs querySelector on the element w/ value provided and sets element to returned value
  * ie. `element = element.querySelector(value)`
* `createImageSubject`
* `replaceStringsWithImages`
* `replaceWithSubject`
* `setStyle`
  * NOTE: at public release you will likely only be able to set certain style properties and/or we might wrap your iframe in a little bit of UI to indicate it was added by Truffle (we’ll need to prevent malicious devs from clickjacking)
* `addStyleSheet`
* `addClassNames`

#### `layout.listenForElements`

```jsx
jumper.call("layout.listenForElements", {
      listenElementLayoutConfigSteps: [
        {
          action: "querySelector",
          value: "ytd-comments#comments ytd-item-section-renderer #contents",
        },
      ],
      observerConfig: { childList: true, subtree: true },
      targetQuerySelector: "ytd-comment-thread-renderer",
      shouldCleanupMutatedElements: true,
    }, onEmit);
```
