---
nav_sort: 2
src: /Documentation/Configurator/Overview.md
---

# Overview

From the Overview page you can:

* View and edit the top-level information and settings of your game.
* Create and manage versions of your game configurations (Snapshots). Publish your game to the live servers.
* Inspect access secrets for your game connection types.
* Create Collaborators for your game and configure their security settings.

![](img/Overview/5.png)

You can use icon button options at the top right of the top panel (highlighted above):

  * ![](/img/fa/heart.png) - Set this game as your favorite. Each time you enter the portal the current game will shown without you having to select it.
  * ![](/img/fa/lock.png) - View your Games Access Secrets.
  * ![](/img/fa/globe.png) - Edit the Geo Restrictions for the game.
  * ![](/img/fa/edit.png) - Edit the top level information regarding your game.
  * ![](/img/fa/trash.png) - Delete this game.


## Editing Top-Level Game Information

![](img/Overview/4.png)

The edit form has the following fields:

  * *Name* \- The name of your game, used to identify the game in the portal if you have several games
  * *Description* \- A description of the game
  * *Primary Region* - Select the geographical region where your game will be published.
  * *Signup Bonuses* \- The amount of each of the currencies to award a new player when a new account is created
  * *Segment Configuration* - Configure Segments for your game. For more details, see [Segments](/Documentation/Configurator/Segments.md).

## Snapshots

![](img/Overview/6.png)

You can use icons button options in the Snapshots panel:

  * ![](/img/fa/plus.png) - Create a new Snapshot of the configuration currently in the portal.
  * ![](/img/fa/copy.png) - Copy this Snapshot to another game.
  * ![](/img/fa/trash.png) - Delete this Snapshot.
  * ![](/img/fa/upload.png) - Publish this Snapshot to the live servers.
  * ![](/img/fa/random.png) - Revert the portal to the version contained in the Snapshot.
  * ![](/img/fa/search.png) - Preview this Snapshot.

Click [here](/Documentation/Key Concepts/Snapshots.md) for more information about Snapshots, Versioning and Publishing.

## Access Secrets

A number of secrets exist for different types of connections:

  * *Device Api Secret* \- Used by your devices to connect to the service as a player.
  * *Server Api Secret* \- Used for callback urls.
  * *SFTP Secret* \- Used for SFTP access for file delivery (Request access via out support system).
  * *Debug Secret* \- Used by the JavaScript remote debugger.

## Collaborators

This area allows the creation of game collaborators, these will be people that can log in with their user and view/edit the game, depending on the security settings set for them. An in-depth tutorial can be found [here](/Tutorials/Capabilities/README.md).
