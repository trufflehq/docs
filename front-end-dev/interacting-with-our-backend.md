# Interacting with our backend

You'll likely want to communicate with our backend, so you can display information for the logged-in user, get and set key-values, use game mechanics, etc...

Because your frontend code is deployed through Truffle, you can use the Truffle API package which provides query methods that are already connected and authenticated with our backend.

Our API package is built as a wrapper around the [urql](https://formidable.com/open-source/urql/) library, so you can refer to its documentation if you need to do anything advanced.

### Performing queries

#### Performing a basic query

To perform a query to our backend, simply import and use the `useQuery` hook provided by the Truffle API package. The following example gets the id, name, and email of the current user.

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



