---
nav_sort: 1
src: /Documentation/Configurator/Integrations/Security Credentials.md
---

# Security Credentials

Credentials allow you to configure permissive role types for Players within the game.  You can configure each Credential to control which requests and responses are authorized for use when connecting to the GameSparks API platform:
* Credentials are passed-in when a connection is made to the platform.
* If you've created a Credential and set it as a Player type, when any player with this Credential connects to the platform the request/response permissions you've configured for the Credential are applied to the player's requests:
  * For example, you might want to set up a Credential which you can use against players to block their access to finding pending Matches (FindPendingMatchesRequest) or allow them only the ability to change their details (ChangeUserDetailsRequest).

To create and edit Credentials, go to *Configurator > Integrations*. Existing Credentials are listed:

![](img/SecCred/2.png)

## Credential settings

There are two ways in which you can configure Credentials for your game:
* Select Credential type.
* Enable Credential requests.

### Selecting Credential Types

When you create or edit a custom Credential there are three key settings you can use to determine the type of Credential and ensure the Credential suits your purposes:
* *Player* - If you select this, it means that the Credential will be used against players. For example, you could use a Player Credential to deny a player access to the matchmaking requests without affecting their permissions to other requests available within the API platform
* *Listener* - If you select this, it means that messages can be passed through to the user.
* *CB* - If you select this, it means that the Credential will be used exclusively for Callback scripts.

There are certain rules applied to the combination of Credential types:
* A Player Credential MUST also be a Listener type.
* However, a Listener Credential does not necessarily need to also be a Player Credential.

<q>**Note:** You cannot alter the type settings for a System Credential!</q>

### Enabling Credential Requests

When you create or edit a Credential, there are four tabs for different requests categories, which you can use to control the requests allowed for the Credential:
* *Requests* - Generic game requests.
* *LogEventRequests* - All Log Event requests including any custom Log Event requests.
* *LogChallengeRequests* - All Challenge Event requests including any custom Challenge Event requests.
* *AdminRequests* - All requests considered to be Administration tasks.

<q>**Note:** *AdminRequests* cannot be enabled for a Player Credential - you will get an error if you try to do this!</q>

## System Credentials

On all games there are five default *System* credentials:
* *Server* - An example Credential for server-to-server communication. By default, this allows a playerId to be sent with the request, and the request would be processed as if it was sent by that player. This Credential is also set up to receive any asyncronous messages sent to any players while connected to the platform.
* *Debug* - This Credential adds JavaScript debugging capabilities to the connection to the platform.
* *Server-send* - Same as the *Server* Credential, except that this Credential doesn't receive asynchronous messages.
* *SFTP* - This Credential gives access to the sftp endpoint, allowing remote systems to deliver files for processing by the platform.
* *Device* - The default Credential you should use in your game. This Credential requires player authentication before requests can be sent.

There are a few important things to note about System credentials:
* You *cannot delete* them.
* You can edit them to configure which requests are allowed.
* You cannot edit for the type of Credential - *Player*, *Listener*, or *CB(Callback)*. These settings are pre-set and locked.
* You can reset the secret for system Credentials, *except* for the *Device* Credential.

### Editing System Credentials

To edit a System Credential:

*1.* Click the edit ![](/img/fa/edit.png) icon. The *Edit Credential* dialog appears:

![](img/SecCred/3.png)


*2.* Select any of the four request tabs and check the individual requests under each one for the Credentials you want to allow/disallow. In this example, the first Requests tab is selected and all requests on this tab are checked and therefore allowed.

*3.* Click *Save* at the bottom of the dialog to save your changes.

## Creating and Editing Custom Credentials

To create and edit a custom Credential:

*1.* Click the plus ![](/img/fa/plus.png) icon. The *Create Credential* dialog appears:

![](img/SecCred/4.png)

*2.* Complete the mandatory fields for the Credential:
* *Short Code* - Unique identifier.
* *Name*
* *Description*

*3.* Use the toggle buttons at top-right to enable the type of Credential you want - *Player*, *Listener*, or *CB*. In this example, we have selected for a *Player* Credential. When you select *Player*:
* *Listener* is automatically selected.
* You cannot select *CB*, because *Player* and *CB* are mutually exclusive Credential types.

*4.* Under the *Requests*, *LogEventRequests*, and *LogChallengeRequests* tabs, check for the requests you want to allow for the Credential.

<q>**AdminRequests.** Remember, *AdminRequests* cannot be selected for a Player Credential!</q>

## Resetting a Credential's Secret

To reset a Credential's secret:

*1.* On the *Credentials* panel, click the reset ![](/img/fa/refresh.png) icon. The *Reset Secret* dialog appears:

![](img/SecCred/5.png)

*2.* Click *Reset* to continue with the Credential secret reset. The *Reset Secret* dialog closes and you'll see that the Credential's secret has been updated:

![](img/SecCred/6.png)

<q>**Callback Example!** For an example of when you might want to create a CB Credential and use it, see the [How to Use Custom Callback Urls](/Tutorials/Cloud Code and the Test Harness/Using Custom Callback Urls.md) tutorial.</q>
