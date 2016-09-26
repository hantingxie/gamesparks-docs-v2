---
nav_sort: 1
src: /Documentation/Key Concepts/Authentication.md
---

# Authentication

Before a player can perform any operations they need to authenticate with the platform. There are a few authentication options, and some can be used in combination with others. These options are described below.

## Username / Password Authentication

Using [RegistrationRequest](/API Documentation/Request API/Authentication/RegistrationRequest.md) you can create a player with a username / password / displayName combination. If you use this method, the player can sign in on any device with the same credentials and will be logged in and their history will be available. Once a player has registered using *RegistrationRequest*, they can use the same userName / password combination with [AuthenticationRequest](/API Documentation/Request API/Authentication/AuthenticationRequest.md) to login to the platform.

## Device Authentication

Perhaps you don't want to force your players to actively login. In these instances, we'll need the ability to identify the device that is being used so we can persist data against the player. To do this, you can perform device authentication. This method registers an identifier (the implementation is dependent on platform) of the device and creates a stub player on the platform.

If you use device authentication, each time the device authenticates it will be identified as the same player and you'll be able to view previous high scores, or use the same playerId in your code.

When using device authentication, there's no display name stored against the player. If you're using Leaderboards, the displayName field of each Leaderboard entry will be blank for these users. You can set a displayName against these anonymous players using *ChangeUserDetailsRequest*, which will set the displayName of the player and also update all Leaderboards to contain the correct displayName.

<q>**Important: Mobile Device Authentication ID!** For mobile device authentication, we strongly recommend that you use an IDFV device ID. Using an IDFA device ID can be unreliable.</q>

## Social Authentication

If you don't want players to create a userName / password combination, you can delegate authentication to one of the social providers. Currently these are:

* [Amazon](/API Documentation/Request API/Authentication/AmazonConnectRequest.md)
* [Facebook](/API Documentation/Request API/Authentication/FacebookConnectRequest.md)
* [Google Plus](/API Documentation/Request API/Authentication/GooglePlusConnectRequest.md)
* [Steam](/API Documentation/Request API/Authentication/SteamConnectRequest.md)
* [Twitter](/API Documentation/Request API/Authentication/TwitterConnectRequest.md)
* [XBOX Live](/API Documentation/Request API/Authentication/XBOXLiveConnectRequest.md)
* [Twitch](/API Documentation/Request API/Authentication/TwitchConnectRequest.md)
* [Kongregate](/API Documentation/Request API/Authentication/KongregateConnectRequest.md)
* [PSN](/API Documentation/Request API/Authentication/PSNConnectRequest.md)
* [Viber](/API Documentation/Request API/Authentication/ViberConnectRequest.md)
* [WeChat](/API Documentation/Request API/Authentication/WeChatConnectRequest.md)
* [QQ](/API Documentation/Request API/Authentication/QQConnectRequest.md)

These methods create a player on the platform and also get their list of friends from the provider. You can then use this list of friends to link players with their friends who also play your game.

Some rules are applied when the player is already authenticated or the social profile is already in use:

* If the player is already authenticated with one of the other methods and the social profile is not already linked to another account, then the social profile will be linked to the current player.
* If the player is already authenticated with one of the other methods but the social profile is already linked to another player, then the client will be logged out of the current account and re-authenticated with the player the social profile is linked to.
* If the player is not already authenticated and the profile is not already in use, then a new player record is created and linked to the social profile.
