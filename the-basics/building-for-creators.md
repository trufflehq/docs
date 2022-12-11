---
description: Here's some of what we've learned from building for creators
---

# Building for creators

### Creators won't put a lot of time in

Everything you build should require as little effort as possible from the creator. Eg. most creators aren't going to want to install software, or go through a long period of setup.

### Spiky traffic (and lots of it)

In a Ludwig stream with \~20,000 viewers, there can be \~8,000 viewers with Truffle installed. Meaning 8,000 concurrent users of the package you've built.

In general we recommend relying on our API as much as possible, since our stacks scales well horizontally, and autoscales up and down depending on how much load there is.

For anything you can't achieve with our API, be very mindful of performance :)

### Viewers will try to find vulnerabilities

Do your best to be sure there isn't a way viewers can cause mayhem - there's a subset of most creators' audience that knows common vulnerabilities (eg number overflow in JS)

### The best ideas tend to be niche

There are so many different types of streamers, and you don't need to build something that's broadly useful for all of them. Find a niche (eg Pokemon streamers) and build something useful for them.
