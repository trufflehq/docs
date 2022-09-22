# Collectibles

Collectibles are used to represent an item that a user can own indefinitely like emotes and tickets or redeem to perform an action like activate a badge in chat or trigger a redemption event that calls your 3rd party server. One thing to note for collectibles is these are a global data types meaning that collectibles can be used across different orgs to open up dynamics like trading and global custom emotes for Truffle creators.

There are 3 different official `type` fields of collectibles:



| type       | Description                                                                                                                                                                                                                                                                                                                             |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| emote      | Emote collectibles represent an emote keyword (slug) and the emote image. When emote collectibles are unlocked they are unlocked indefinitely and users can use them in Truffle features that support emotes like the Community forum and in chat on YouTube and Twitch with the [Truffle.TV](https://truffle.vip/extension) extension. |
| redeemable | Redeemable collectibles can be used to execute an action when the collectible is redeemed. Redeemable collectibles are used to activate some sort of side effect after redeeming the collectible like activating a custom badge in chat, unlocking a custom Discord role, or opening an emote pack.                                     |
| ticket     | Ticket collectibles are used to keep track of entries to something like a giveaway.                                                                                                                                                                                                                                                     |

Here’s a guide for creating a basic emote collectible:

[How to create an emote Collectible?](https://www.notion.so/How-to-create-an-emote-Collectible-f09c8c1b2a484e258b85843f58969fb2)

`redeemable` collectibles are a way to expose functionality where a user can unlock a collectible and then trigger a side effect when the collectible is redeemed. Some examples of redeemable collectibles are activating a powerup, unlocking a discord role, or broadcasting an event topic which can be used to let a 3rd party server know that a collectible has been redeemed.

Here are the supported `redeemType` fields.

#### powerup

`powerup` redeemType collectibles can be used to activate a Truffle powerup.

`redeemData` schema:

```json
"redeemData": {
	“powerupId”: <powerupId>,
	“duractionSeconds”: <no. seconds>
}
```

#### alertCustomMessage

Used to trigger an alert. An example of this is having an OBS overlay where users can redeem a collectible and trigger an alert in the overlay.

The user’s input for the message will be passed in to the `ownedCollectibleRedeem` mutation as the `additionalData` parameter

#### collectiblePack

The collectiblePack is similar in concept to a trading card pack in that the developer will specify a list of collectibles that can be awarded when the collectiblePack is opened with a series of odds and when the pack is redeemed (opened), the user will be randomly awarded the collectible based on the odds specified by the developer.

`redeemData` schema:

```json
"redeemData": {
    "collectibleRels": [
      {
        "id": "<collectible1Id>",
        "odds": 0.33
      },
      {
        "id": "<collectible2Id>",
        "odds": 0.16
      },
      {
        "id": "<collectible3Id>",
        "odds": 0.5
      },
      {
        "id": "<collectible4Id>",
        "odds": 0.01
      }
    ]
  }
```

#### event

This redeemType is used to emit a side effect to 3rd party apps and integrations. This lets devs create collectibles that they’re bespoke service can subscribe to.

`redeemData` schema:

```json
"redeemData": {
	"eventTopicPath": "@truffle/viewer-polls@latest/_EventTopic/viewer-create-poll"
}
```

where eventTopicPath is the human readable EventTopic.

#### recipe

Recipes are used to redeem multiples of a collectible to an upgraded collectible. This model is used to handle emote upgrades e.g rainbow emote upgrades where you can redeem N of an to unlock 1 of the rainbow emotes.

```json
"redeemData": {
    "recipe": {
      "inputs": [
        {
          "isVariable": true,
          "amountType": "collectible",
          "amountIds": [
            "6a09ebf0-9919-11ec-9f1b-3f9388789914",
            "3d4e8170-9919-11ec-9f1b-3f9388789914",
            "c3be5ba0-9918-11ec-9f1b-3f9388789914",
            "ab9df340-ecd4-11ec-be53-8611511c5353"
          ],
          "amountValue": 3
        }
      ],
      "outputs": [
        {
          "outputType": "collectible",
          "outputIdFromVariableAmountId": {
            "6a09ebf0-9919-11ec-9f1b-3f9388789914": "6c006cf0-dad1-11ec-a72a-ebd11b17495b",
            "3d4e8170-9919-11ec-9f1b-3f9388789914": "40533e20-dad1-11ec-a4bf-31ad272ca615",
            "c3be5ba0-9918-11ec-9f1b-3f9388789914": "8b497570-dad1-11ec-9101-6e068b6d8d6a",
            "ab9df340-ecd4-11ec-be53-8611511c5353": "02ca0300-ecd7-11ec-bd4d-2502ad5d33f1"
          }
        }
      ]
    }
  }son
```



Here’s a guide for creating a collectible that activates a powerup when it’s redeemed:

[How to create a redeemable Collectible that activates a powerup?](https://www.notion.so/How-to-create-a-redeemable-Collectible-that-activates-a-powerup-c6fccdb150524940b07a390e2b8154e9)

Here’s a guide for creating a collectible that broadcasts a custom event topic when it’s redeemed:

[How to create a collectible that broadcasts a custom event topic?](https://www.notion.so/How-to-create-a-collectible-that-broadcasts-a-custom-event-topic-2bddb4c484874fb3a88a6d514c270230)

Here’s a guide for creating recipe collectibles to convert duplicate collectibles into an upgraded version:

[How to create a recipe collectible?](https://www.notion.so/How-to-create-a-recipe-collectible-b2bdc51bb1414d08b8e14b2330635a42)

To keep track of user ownership of collectibles we have the [OwnedCollectible](https://www.notion.so/Owned-Collectible-4c88e35706044a4397e51a63a1771164) model.

Currently the built-in methods for giving a user a collectible are through the SeasonPass or a `channelPointsStorePurchase` EconomyAction.

If you’d like to manage this process yourself in your application you can give a user a collectible with the `[ownedCollectibleIncrement](<https://www.notion.so/Owned-Collectible-4c88e35706044a4397e51a63a1771164>)` mutation.

Here’s a guide for giving a user a collectible.

[How to give a user a collectible?](https://www.notion.so/How-to-give-a-user-a-collectible-3c4dbdf821bf46a2bbb284f83d53dbb3)

If you’re building a front-end to let users redeem collectibles you can manage this flow with the `[ownedCollectibleRedeem](<https://www.notion.so/Owned-Collectible-4c88e35706044a4397e51a63a1771164>)` mutation.

Here’s a guide for redeeming an OwnedCollectible

[How to redeem an owned collectible?](https://www.notion.so/How-to-redeem-an-owned-collectible-c4bf6c7282ed4c43aa70a2f82717e166)

