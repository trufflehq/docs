# Truffle.TV Embeds

Building Embeds are how you can add functionality to creators' content through [the browser extension.](https://chrome.google.com/webstore/detail/mogultv/bkkjeefjfjcfdfifddmkdmcpmaakmelp)

#### Quick extension overview

The core of the extension itself is fairly lightweight. It serves two main purposes:

1. Adding iframes/widgets to a page (we call them "Embeds")
   1. eg. Adding a menu for channel points and predictions to a YouTube stream
2. A mutation observer and light modification/styling of DOM elements in a page
   1. eg. Observing new chat messages and replacing strings in the message body with emotes

#### Setting up your first embed

{% embed url="https://youtu.be/zGLuD8knFro" %}

#### Testing

* Visit test stream: [https://www.youtube.com/watch?v=Xe5KJINZGRA](https://www.youtube.com/watch?v=Xe5KJINZGRA)
  * Open extension menu (Ludwig’s face)
  * Click settings cog
  * Click on bottom right of menu to bring up secret dev options
  * Enter your URL: `https://<packageVersionId>.sporocarp.dev/embed`
    *   Unfortunately [localhost](http://localhost) won’t work since it’s insecure content (http iframe inside an https page)

        * You can get it to work if you launch chrome in insecure mode:

        ```jsx
        /Applications/Google\\ Chrome.app/Contents/MacOS/Google\\ Chrome --allow-running-insecure-content </dev/null &>/dev/null &
        ```
  * Save and refresh

### Jumper

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
