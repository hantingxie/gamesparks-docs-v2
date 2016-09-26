---
nav_sort: 6
src: /Documentation/Key Concepts/Social Capabilities.md
---

# Social Capabilities

The GameSparks platform allows you to make use of players' existing social media relationships to build a truly social gaming experience.

## Connecting

The platform exposes social API calls, which you can use to connect your players with their social profiles. This allows the platform to get data about your players on your behalf and gives the platform access to information such as friend lists. Connecting is the first step towards utilizing the platform's social capabilities.

## Inviting

You can use [ListInviteFriendsRequest](/API Documentation/Request API/Player/ListInviteFriendsRequest.md) to get a list of those friends of your current players who are not yet playing your game. You can then encourage your players to get these non-playing friends to play your game. This kind of social propagation is key for getting awareness of your game to spread virally.

## Matching

You can use [ListGameFriendsRequest](/API Documentation/Request API/Player/ListGameFriendsRequest.md) to get a list of friends of your current players who are already players of your game. This allows you to match up players and encourage them to chat to their friends and challenge each other.

## Chatting

You can use [SendFriendMessageRequest](/API Documentation/Request API/Player/SendFriendMessageRequest.md) to send messages between two players that are friends. For more information on the messaging capabilities provided by the GameSparks platform, see [Messaging](/Documentation/Key Concepts/Messaging.md).

## Ranking

Leaderboard data for players that are linked as friends will contain not only their global position within the Leaderboard but also a social rank, relative only to their friends. This lets players compete against their friends as well as against the wider population. Achievements can be awarded based on social rankings, which means players are competing against a much smaller population for those precious awards!

For more information on Leaderboards within the GameSparks platform, see [Leaderboards](/Documentation/Configurator/Leaderboards.md).
