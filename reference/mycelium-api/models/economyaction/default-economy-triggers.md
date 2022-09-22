# Default Economy Triggers

Here is a list of the built in Economy Triggers with their hard-coded IDs inside of Truffle.

| slug                              | id                                   | Description                                                                                                               |
| --------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| tier-unlock                       | 85e9ed40-d73d-11ec-97bc-651463e09eec | Used to update a user’s SeasonPassProgression tier. e.g if a user purchases the premium tier of a battle pass.            |
| forum-create-post                 | 3a2de150-6f68-11ec-b706-956d4fcf75c0 | A user create a post in the forum                                                                                         |
| forum-react-to-post               | 3c07f880-6f68-11ec-b706-956d4fcf75c0 | A user reacts to a post in the forum                                                                                      |
| forum-comment-on-post             | 3e0d8c80-6f68-11ec-b706-956d4fcf75c0 | A user comments on a post in the forum                                                                                    |
| forum-reactions-to-post           | 3f777cc0-6f68-11ec-b706-956d4fcf75c0 | A post a user created gets N number of reactions in the forum                                                             |
| xp-extension-increment            | b9d69a60-929e-11ec-b349-c56a67a258a0 | A trigger to increment a user’s XP for passive watch time in the Truffle.TV extension                                     |
| xp-extension-claim                | fc93de80-929e-11ec-b349-c56a67a258a0 | A trigger to increment a user’s XP for clicking the claim button in the Truffle.TV extension                              |
| channel-points-increment          | 40ab1ac0-6f68-11ec-b706-956d4fcf75c0 | A trigger to increment a user’s Channel Points for passive watch time in the Truffle.TV extension                         |
| channel-points-claim              | 41760be0-6f68-11ec-b706-956d4fcf75c0 | A trigger to increment a user’s Channel Points for clicking the claim button in the Truffle.TV extension                  |
| channel-points-purchase           | 4246f070-6f68-11ec-b706-956d4fcf75c0 | A trigger to indicate that a product in the Channel Points shop is being purchased.                                       |
| channel-points-prediction         | 43477080-6f68-11ec-b706-956d4fcf75c0 | A trigger to execute an EconomyAction to place a user prediction with a variable amount of user specified channel points. |
| channel-points-prediction-win     | 5807bc10-80c4-11ec-a5c9-01fed7cc1cdc | A trigger to execute an EconomyAction to pay out a user if they won a prediction                                          |
| channel-points-prediction-refund  | e3e4e4a0-b2bb-11ec-9571-dd01980fb9d3 | A trigger to execute an EconomyAction to refund a user if a prediction was cancelled                                      |
| channel-points-admin-modification | ddd60d00-d17e-11ec-b0a8-ab7476fd20c7 | A trigger to execute an EconomyAction for an admin modification to a user’s channel points.                               |
