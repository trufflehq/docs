# How packages are used

### How creators (and other developers) use components

#### Creators (website builder GUI)

**Website**

When a creator signs up, we fork a “default site” package that has some basic pages. Each page is a component, and those components can hold other components (think of it like a grid layout, where a component can go in each block).

![](<../../.gitbook/assets/unknown (8).png>)

So when a creator sets up their site, they can use components you’ve built

**Extension**

Another example would be in the browser extension. Your components can either exist inside of the UI for another package’s component (eg as a tab in Mogul Menu, the menu most creators are using for predictions, channel points, etc…)

#### Other developers

We anticipate some developers creating themes for creator sites. We also anticipate creators having developers on their teams to build more custom experiences.

This means other developers may use your components via code. The process is pretty straight-forward - they import your components and include it in theirs (regardless of the runtime their package is using - React, Vue, Svelte, etc…). Web Components make this easy!

### Deploying for creators

#### React Components vs Web Components

We see a future where [Web Components](https://www.webcomponents.org/introduction) are the norm and all the major frameworks have easy exports to them.

React is the most developed ecosystem today, so all of our examples use React, but we support components built in Vue, Svelte, Lit, etc… So you’ll likely be building components in React, in order for other creators to use them, you’ll be exporting as Web Components. Don’t worry, we make this easy!

Web Components are also great at encapsulation. Your styles and DOM attributes won’t leak into other components and their styles/DOM attributes won’t affect into yours :) And we aren’t stuck with a single React version until the end of eternity - it may not be ideal from a file-size/loading perspective, but components can use different major versions of React.

**Limitations:**

* toDist relies on defining the PropTypes for the component
* toDist in React currently doesn’t support function props, just primitive types / objects

#### Making certain components public (entry files)

You probably don’t want _every_ component you make to be available for creators to add from your package. You also might not want to make every component a Web Component. So the only components that will be made available to creators that have installed/purchased your package are component files named \*`file-name*.entry.js`

#### Entry file requirements

* Must export a Web Component as the default export
* Must specify PropTypes for all props creators should be allowed to edit
* The React Component definition, PropTypes and export must all be in the same file
