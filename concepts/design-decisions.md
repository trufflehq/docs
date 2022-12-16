# Design decisions

### Web components

We want to create a flexible ecosystem where multiple packages can  coexist together in extension embeds and creator websites. Web Components are a great tool for this.

Web Components encapsulate styles, so one package's CSS won't conflict with another's. They also allow us to be framework-agnostic and have components created with different frameworks (React, Vue, Svelte, etc...), plus components created with different versions of the same framework running in the same page/view.

With that said, Web Components today aren't the easiest tool for building websites - frameworks like React and Vue are - and fortunately those frameworks mostly support exporting to web components.

### URL Imports

Still with the mindset of having a flexible ecosystem for multiple packages, we wanted to get rid of any type of build step. So we defer the "build" step, and bundle on request instead.

TODO: we'll explain this better

We also plan to give creators and their teams a code-free interface for adding packages / components to their site / extension.&#x20;

### GraphQL

Developer experience

### Live Queries

Developer experience, theoretically less server load than polling

