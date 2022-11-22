# Using the Mutation Observer

{% embed url="https://youtu.be/jYxjOM0S0pI" %}

See the [Chants package](https://github.com/trufflehq/truffle-packages/blob/master/examples/chants/components/chants/chant.tsx) for an example



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
