---
description: What to setup and install to start building your first app!
---

# Getting Started

So, you want to build a Truffle App.&#x20;

You'll need to do a few things to get started

* Install the [Truffle Browser Extension](https://truffle.vip/extension)
* Install the [Truffle CLI](https://github.com/trufflehq/truffle-cli#installing)
* Create a web app in the framework of your choice
* Install the [Truffle SDK](https://www.npmjs.com/package/@trufflehq/sdk) in your project

## Installing the Extension

First things first, you'll need the Truffle browser extension. You can download that here [https://truffle.vip/extension](https://truffle.vip/extension).  Firefox or any chromium browser (chrome, edge, opera, brave, etc) should work, although only Chrome and Firefox are officially supported.

Now that the Truffle extension is installed you'll have access to the truffle devtools! You can access the devtools by clicking inspect element and then navigating to the devtools\


<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Click the three dots to see hidden tabs</p></figcaption></figure>

very cool, you'll use this interface later

<img src="../.gitbook/assets/image (7).png" alt="" data-size="original">

## Installing the Truffle CLI

To get a user auth token for your app, you'll need to install the Truffle CLI.

**\*\*Truffle CLI does not support windows right now, so you'll need to use WSL\*\***\
[https://learn.microsoft.com/en-us/windows/wsl/install](https://learn.microsoft.com/en-us/windows/wsl/install)&#x20;

If you don't have yarn or npm installed choose one and install

npm: [https://docs.npmjs.com/downloading-and-installing-node-js-and-npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) \
yarn: [https://yarnpkg.com/getting-started/install](https://yarnpkg.com/getting-started/install)&#x20;

Install the CLI globally with:

```bash
yarn global add @trufflehq/cli
```

or with npm

```bash
npm install -g @trufflehq/cli
```

if you previously installed the CLI, make sure `truffle-cli --version` is 0.3.3 or higher.&#x20;

## Choosing a framework

Now you get to choose what framework you want to build your App in! So create a project in your framework of choice, or install what we'll be using for all our tutorials: Vite with React + Typescript

#### Installing Vite

If you chose a different framework, you don't need to install Vite

To install with yarn:

```bash
$ yarn create vite@latest
```

Or, with npm

```bash
$ npm create vite@latest
```

Choose a project name (or keep the default name lol), select React as your framework, and then TypeScript and then follow the instructions to run your project.

<figure><img src="../.gitbook/assets/image (4).png" alt="" width="369"><figcaption><p>Instructions that are printed after you <code>yarn create vite@latest</code></p></figcaption></figure>

## Installing the SDK

The last thing you'll need to install is the Truffle SDK

The SDK is an npm package that can be added as a dependency to your project with npm or yarn

```shell
npm install @trufflehq/sdk
```

or if you are a yarn enjoyer

```shell
yarn add @trufflehq/sdk
```

And that's it, you now have everything you need to develop a Truffle app!



Now lets build something ->\








