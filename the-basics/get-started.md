---
description: It only takes a few commands to start developing a package!
---

# Getting Started

## Getting started

{% embed url="https://youtu.be/XU9RzvP48jU" %}

#### Get an API key

We will give you an API key you can use. If you don’t have one, we’re still working through the developer waitlist. Once you have an API key, you're golden and can run through the rest of the documentation!

#### Install truffle-cli

```bash
npm i -g @trufflehq/cli
```

or

```bash
yarn global add @trufflehq/cli
```

#### Authenticate

```bash
truffle-cli auth <secretKey>
```

#### Create your first package

```bash
truffle-cli create <package-slug>
cd <package-slug>
```

{% hint style="info" %}
Everything you build in Trufle will be a package. Think of them as "apps" or "products".&#x20;

Creators will be able to install your package into their site package

For example, the "Myth" organization has a "site" package that serves up mogul-menu (the extension menu package with channel points, etc...), raid-overlay, and a few other packages.
{% endhint %}

#### Run dev server

```bash
truffle-cli dev
```

Visit [http://localhost:8000](http://localhost:8000)

#### Deploying

```bash
truffle-cli deploy
```

This will give you a URL you see your package at.

****

**Huzzah!**

You're ready to get building for creators! Head on over to the frontend-dev [introduction.md](../front-end-dev/introduction.md "mention") next :)

****
