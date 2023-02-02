# Truffle Data in Embeds

This tutorial will teach you how to create a Truffle Embed that can read and display user information using React and the Truffle SDK.&#x20;

The final product will be a simple embed, displaying the streamer's org name and image as well as the user’s display name and avatar image.

## Set Up&#x20;

You should have successfully created a Truffle Embed with React and Typescript following the instructions on the [getting-started.md](getting-started.md "mention") page.

## Getting Data From the Truffle SDK

First we are going to get data from the SDK the hard way using [ECMA Observables](https://github.com/tc39/proposal-observable), then show the easier method using [Legend-State](https://legendapp.com/open-source/state/)&#x20;

### Importing the SDK

For this tutorial we will use the following:

```javascript
import {
  org as orgClient,
  user as userClient,
  getSrcByImageObj,
} from "@trufflehq/sdk";
```

`user` and `org` both give us ECMA Observables

`getSrcByImageObj` will be useful later when we want to get the avatar images

### Using ECMA Observables

Import `useEffect` and `useState` from React

Create a new state variable to keep track of the observables' value. In this case we are going to track Org ID

```tsx
const [orgId, setOrgId] = useState<string | undefined>(undefined);
```

Now subscribe to the observable inside a `useEffect` so we can update the orgId state

```tsx
// this is how you use spec compliant observables without legend
useEffect(() => {
  const subscription = orgClient.observable.subscribe({
    next: (org) => {
      // this is called every time the value changes
      setOrgId(org.id);
    },
    error: (error) => {
      console.error(error);
    },
    complete: () => {}
  })
  return () => subscription.unsubscribe()
})
```

This is all we need to use `orgId` in the app

```tsx
return (
  <div className="App"> 
    <div>Org ID: {orgId}</div>
  </div>
);
```

Save the file and you should see the Org ID show up in the Embed!

### Using Legend Observables

Install Legend

```bash
npm install @legendapp/state
```

Then import Legend into the project

```tsx
import { observer } from "@legendapp/state/react";
```

Download or copy and paste this function that can convert native ECMA observables to Legend observables. Eventually we hope that this function gets baked into legend itself but right now you will just need to download it yourself from the link below:

[https://github.com/trufflehq/truffle-packages/blob/master/npm/sdk/examples/react-auth/src/from-spec-observable.ts](https://github.com/trufflehq/truffle-packages/blob/master/npm/sdk/examples/react-auth/src/from-spec-observable.ts)

Import the function

```tsx
import { fromSpecObservable } from "./from-spec-observable";
```

Then we can use this function to convert all the observables we imported from the Truffle SDK

```tsx
const org = fromSpecObservable(orgClient.observable);
const user = fromSpecObservable(userClient.observable);
const orgUser = fromSpecObservable(userClient.orgUser.observable);
```

Now we can simple call `.get()` and use the value in the JSX!

```tsx
return (
  <div className="App">
    <div>Org: {org.name.get()}</div>
    <div>Org ID: {orgId}</div>
    <h2>Welcome, {orgUser.name.get()}</h2>
    <img src={getSrcByImageObj(user.avatarImage.get(), { size: "small" })} />
  </div>
);
```

This won't quite work yet because we need to wrap the react component export in the observer

```tsx
export default observer(App);
```

Now you should be able to use these variables in whatever way you want!

Here is the complete react component for reference:

```tsx
import "./App.css";
import {
  org as orgClient,
  user as userClient,
  getSrcByImageObj,
} from "@trufflehq/sdk";
import { observer } from "@legendapp/state/react";
import { fromSpecObservable } from "./from-spec-observable";
import { useEffect, useState } from "react";

const user = fromSpecObservable(userClient.observable);
const orgUser = fromSpecObservable(userClient.orgUser.observable);
const org = fromSpecObservable(orgClient.observable);

function App() {
  const [orgId, setOrgId] = useState<string | undefined>(undefined);
  useEffect(() => {
    const subscription = orgClient.observable.subscribe({
      next: (org) => {
        setOrgId(org.id);
      },
      error: (error) => {
        console.error(error);
      },
      complete: () => {}
    })
    return () => subscription.unsubscribe()
  })

  return (
      <div>Org: {org.name.get()}</div>
      <div>Org ID: {orgId}</div>
      <h2>Welcome, {orgUser.name.get()}</h2>
      <img src={getSrcByImageObj(user.avatarImage.get(), { size: "small" })} />
    </div>
  );
}

export default observer(App);

```
