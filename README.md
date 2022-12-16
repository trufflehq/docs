---
description: Want to know what you can build and how to build it? You're in the right place
---

# Overview

## Welcome!

Welcome to the Truffle Developer Platform - we’re stoked you’re here!

We’re building out the infrastructure that’ll make it easy for you to build cool shit for creators :)

**Want to jump straight to building? Head over to** [get-started.md](the-basics/get-started.md "mention")!

## "What can I build?"

**To start, we're making it easy for you to build "apps" (we call them "packages") that creators can use in their stream.** Think of a Truffle package as a more powerful Twitch extension, that works for YouTube and Twitch streamers.

You'll be able to charge for these packages (if you want!). And in the early days we'll work on other incentives like bounties (ideas we know creators want, that we'll pay to have built)

## "How do I build?"

We have 3 toolsets you can use to build these packages:

#### 1) Frontend framework

This is a simple frontend framework that allows you to write components in React and deploy them to Truffle's hosting infrastructure.

It's complete with file-system-based routing, a dev server, and the ability to use React (and eventually other frameworks like Vue, Svelte, etc...)

Your frontend code will be able to embed itself into YouTube and Twitch livestreams, and control various parts of the page (to be able to position your element, tweak styles on chat messages, etc...)

#### 2) GraphQL API

This will let you hook into our backend for working with users, collectibles, channel points, roles, permissions, etc...

In an ideal world most packages will be built without needing to build your own custom backend. Though it may take some time for the API to become flexible enough for all types of ideas.

#### 3) Edge Functions

For anything you can't achieve with our GraphQL API, you can use our hosted Edge Functions (aka serverless). We host these so you don't have to pay for hosting, and tie everything together with our truffle-cli



{% hint style="info" %}
The developer platform and these docs are still in a very early stage of development. Please let us know where we can improve!
{% endhint %}
