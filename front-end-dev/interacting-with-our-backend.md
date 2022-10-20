# Interacting with our backend

You'll likely want to communicate with our backend, so you can display information for the logged-in user, get and set key-values, use game mechanics, etc...

Because your frontend code is deployed through Truffle, we contextualize requests and server-render basic information like the Org ID, making it readily available for your code when the page loads. You can use the Truffle API package which provides query methods that are already connected and authenticated with our backend.

Our API package is built as a wrapper around the [urql](https://formidable.com/open-source/urql/) library, so you can refer to its documentation if you need to do anything advanced.

### Performing queries

#### Performing a basic query

To perform a query to Mycelium, simply import and use the `useQuery` hook provided by the Truffle API package. The following example gets the id, name, and email of the current user.

```tsx
import React from "https://npm.tfl.dev/react";
import { gql, useQuery } from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";

const ME_QUERY = gql`
  query {
    me {
      id
      name
      email
    }
  }
`;

export default function MeInfo() {
  // execute the query
  const [{ data, fetching, error }] = useQuery({ query: ME_QUERY });

  // extract the `me` object from the response
  const me = data?.me;

  return (
    <>
      {/* display a loading message while we fetch data from the server */}
      {fetching && "Loading..."}

      {/* display the result when we're done fetching */}
      {!fetching && (
        <>
          {/* display the user info if we get it */}
          {me && (
            <div>
              <div>ID: {me.id}</div>
              <div>Name: {me.name}</div>
              <div>Email: {me.email}</div>
            </div>
          )}

          {/* display any errors if we get any */}
          {error && <div>Error: {JSON.stringify(error)}</div>}
        </>
      )}
    </>
  );
}
```

{% hint style="info" %}
In some editors, including VSCode, the `gql` tagged template literal will enable syntax highlighting for the query.
{% endhint %}

#### Using variables

If you need to pass variables to your query, simply pass it via the `variables` prop in the argument to `useQuery`. In the following example, we are creating an `UserInfo` component that will display information about an arbitrary user.

```tsx
import React from "https://npm.tfl.dev/react";
import { gql, useQuery } from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";

const ORG_USER_QUERY = gql`
  query($input: UserInput) {
    user(input: $input) {
      id
      name
    }
  }
`;
export default function UserInfo({ userId }) {
  const [{ data, fetching, error }] = useQuery({
    query: ORG_USER_QUERY,
    variables: {
      input: {
        id: userId,
      },
    },
  });

  const user = data?.user;

  return (
    <>
      {/* display a loading message while we fetch data from the server */}
      {fetching && "Loading..."}

      {/* display the result when we're done fetching */}
      {!fetching && (
        <>
          {/* display the user info if we get it */}
          {user && (
            <div>
              <div>ID: {user.id}</div>
              <div>Name: {user.name}</div>
              <div>Date joined: {user.time}</div>
            </div>
          )}

          {/* display any errors if we get any */}
          {error && <div>Error: {JSON.stringify(error)}</div>}
        </>
      )}
    </>
  );
}
```

#### Using query observables

Observables are a common pattern used in front end development and popularized by the [RxJS](https://rxjs.dev/) library. If you want the result of your query to come in the form of an observable, use the `queryObservable` method from the API package. Then you can extract the latest value from the observable using the `useObservables` hook from the API package. The next example shows the `UserInfo` component rewritten using the observable pattern.

```tsx
import React from "https://npm.tfl.dev/react";
import {
  gql,
  queryObservable,
} from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";
import useObservables from "https://tfl.dev/@truffle/utils@0.0.3/obs/use-observables-react.ts";

const ORG_USER_QUERY = gql`
  query($input: UserInput) {
    user(input: $input) {
      id
      name
    }
  }
`;

export function UserInfo({ userId }) {

  // use the `useObservables` hook to extract the latest value from an observable
  const { result } = useObservables(() => ({
    // create an observable for our query to Mycelium;
    // queryObservable(query, varaiables)
    result: queryObservable(ORG_USER_QUERY, { input: { id: userId } }),
  }));

  const error = result?.error;
  const fetching = !result?.data && !error;
  const user = result?.data?.user;

  return (
    <>
      {/* display a loading message while we fetch data from the server */}
      {fetching && "Loading..."}

      {/* display the result when we're done fetching */}
      {!fetching && (
        <>
          {/* display the user info if we get it */}
          {user && (
            <div>
              <div>ID: {user.id}</div>
              <div>Name: {user.name}</div>
              <div>Date joined: {user.time}</div>
            </div>
          )}

          {/* display any errors if we get any */}
          {error && <div>Error: {JSON.stringify(error)}</div>}
        </>
      )}
    </>
  );
}
```

#### Performing successive queries

Sometimes you might need to make a query with variables that depend on the result of another query. In this case, you can use an observable with the `switchMap` operator to execute a query when the result of another query becomes available.

// TODO: think of simple example for this

#### Polling queries

Sometimes you expect some data to change inside of Mycelium without the user taking some kind of action. In cases like these, you might want to poll Mycelium for some data. Fortunately, there is a `usePollingQuery` method that makes polling easy. In the next example, we expect that a particular OrgUserCounter "followers" will change when other users follow them, so we poll for its value.

```tsx
import React from "https://npm.tfl.dev/react";
import {
  gql,
  usePollingQuery,
} from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";

const FOLLOWER_QUERY = gql`
  query {
    # get the type of the counter
    orgUserCounterType(input: { slug: "follower-count" }) {
      # get the counter for the signed in user
      orgUserCounter {
        count
      }
    }
  }
`;

const POLL_INTERVAL_MS = 1000;

export default function FollowerCount() {
  // initialize the polling query
  const { data, fetching, error } = usePollingQuery(POLL_INTERVAL_MS, {
    query: FOLLOWER_QUERY,
  });

  const followerCount = data?.orgUserCounterType?.orgUserCounter?.count;

  return (
    <>
      {/* display a loading message while we fetch data from the server */}
      {fetching && "Loading..."}
      {/* display the result when we're done fetching */}
      {!fetching && (
        <>
          {/* display the user info if we get it */}
          {followerCount && <div>{followerCount} followers</div>}

          {/* display any errors if we get any */}
          {error && <div>Error: {JSON.stringify(error)}</div>}
        </>
      )}
    </>
  );
}
```

#### Polling query observables

You can also use create a polling query using the observable pattern.

```tsx
import React from "https://npm.tfl.dev/react";
import {
  gql,
  pollingQueryObservable,
} from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";
import useObservables from "https://tfl.dev/@truffle/utils@0.0.3/obs/use-observables-react.ts";

const FOLLOWER_QUERY = gql`
  query {
    # get the type of the counter
    orgUserCounterType(input: { slug: "follower-count" }) {
      # get the counter for the signed in user
      orgUserCounter {
        count
      }
    }
  }
`;

const POLL_INTERVAL_MS = 1000;

function FollowerCount() {
  // initialize the polling query
  const { result } = useObservables(() => ({
    // pollingQueryObservable(interval, query, variables)
    result: pollingQueryObservable(POLL_INTERVAL_MS, FOLLOWER_QUERY),
  }));

  const error = result?.error;
  const fetching = !error && !result?.data;
  const followerCount = result?.data?.orgUserCounterType?.orgUserCounter?.count;

  return (
    <>
      {/* display a loading message while we fetch data from the server */}
      {fetching && "Loading..."}
      
      {/* display the result when we're done fetching */}
      {!fetching && (
        <>
          {/* display the user info if we get it */}
          {followerCount && <div>{followerCount} followers</div>}

          {/* display any errors if we get any */}
          {error && <div>Error: {JSON.stringify(error)}</div>}
        </>
      )}
    </>
  );
}
```

### Executing mutations

To execute a mutation, you'll first retrieve a mutation function from the `useMutation` hook, then you can call that function from a callback inside your component. In the following example, we are building a button that allows the user to vote on an option in a [Poll](../mycelium-api/features/user-interaction/polls.md).

```tsx
import {
  gql,
  useMutation,
} from "https://tfl.dev/@truffle/api@~0.1.0/client.ts";
import Button from "https://tfl.dev/@truffle/ui@~0.1.0/components/button/button.tag.ts";

const VOTE_MUTATION = gql`
  mutation PollVote($input: PollVoteByIdInput!) {
    pollVoteById(input: $input) {
      hasVoted
    }
  }
`;

export default function PollVoteButton({ pollId, pollOptionIdx }) {
  // retrieve the mutation function
  const [_voteResult, executePollVoteMutation] = useMutation(VOTE_MUTATION);

  const clickHandler = async () => {
    // pass in variables when you execute the mutation
    const { error } = await executePollVoteMutation({
      input: {
        id: pollId,
        optionIndex: pollOptionIdx,
      },
    });

    if (error) {
      alert(JSON.stringify(error));
    }
  };

  return <Button onClick={clickHandler}>Option {pollOptionIdx}</Button>;
}
```



