# Introduction

We built an easy way for you to use React (and eventually any web framework) to build components that can be embedded in the extension.

Our front-end dev process should hopefully feel a little bit like using Next.js, just with our own unique spin to best support creators and a broader package ecosystem.

Be sure to follow the steps in [get-started.md](../the-basics/get-started.md "mention") first, to install truffle-cli and create your first package.

## What's the frontend code for?

We anticipate most early usage of the Truffle developer platform will be adding functionality to the Truffle.TV extension, with some UI for viewers to interact. And for ideas that don't involve viewer interaction, you'll likely still want to build some sort of interface for mods and the creators to manage settings.

## Dev server

`truffle-cli dev`

This will spin up a local dev server that can be accessed at [http://localhost:8080](http://localhost:8080/)

## Using React



## Routing

We use filesystem-based routing. So if you want to add another route, just create a new folder in `/routes` and a `page.tsx` file inside the route.

## Deploying

`truffle-cli deploy`

## What's different

### Web Components

You may noticed that all routes wrap their export in a `toDist` function. This converts the React component to a Web Component.

**You don't need to learn how Web Components work** - we realize most developers will just be writing pure React code, but if you're curious, we use Web Components because of their CSS encapsulation, and ability to be framework-agnostic. This enables you to use frameworks other than React, or different versions of React, without the entire page blowing up :)

### URL Imports

Instead of having a package.json file and installing packages from npm, we use URL imports.&#x20;
