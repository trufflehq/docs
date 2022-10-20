---
description: It only takes a few commands to start developing a package!
---

# Getting Started

## Getting started

{% embed url="https://youtu.be/XU9RzvP48jU" %}

#### Get an API key

We will give you an API key you can use. If you don’t have one, we’re still working through the developer waitlist

#### Install truffle-cli

```bash
npm i -g trufflehq/truffle-cli
```

or

```bash
yarn global add trufflehq/truffle-cli
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

Or: `truffle-cli watch` to update when files get saved
