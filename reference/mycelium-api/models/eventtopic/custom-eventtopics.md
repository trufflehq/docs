# Custom EventTopics

The `event` redeemType allows developers to define collectibles that users can redeem and will broadcast an event topic that developers can subscribe to on their own servers and serverless functions.

Before creating the collectible, you will need to create a custom event topic that the collectible will broadcast when the collectible is redeemed. Check out this article to learn how to create the corresponding custom event topic.

```graphql
mutation CollectibleUpsert ($input: CollectibleUpsertInput!) {
  collectibleUpsert(input: $input) {
    collectible {
      id
      name
      type
    }
  }
}
```

```json
{
	"input": {
	  "name": "Create a poll",
	  "slug": "viewer-create-poll",
	  "type": "redeemable",
	  "data": {
	    "redeemType": "event",
	    "redeemButtonText": "Redeem",
	    "redeemData": {
	      "eventTopicPath": "@truffle/events-demo-backend@latest/_EventTopic/viewer-create-poll"
	    }
	  }
	}
}
```

This query will create a collectible that will broadcast a custom event topic `viewer-create-poll` when a user redeems the collectible.

Note that in the collectible `redeemData` we set an `eventTopicPath` field that represents a human readable string for a custom `viewer-create-poll` event topic.
