---
nav_sort: 2
src: /Documentation/Game Overview/README.md
---

# Game Overview

From the Game Overview page you can:

* View and edit the top-level information and settings of your game.
* Create and manage versions of your game configurations (Snapshots).
* Publish Snapshots of your game to the live servers.
* Inspect access secrets for your game connection types.
* Create Collaborators for your game and configure their security settings.

![](img/GameOverview/7.png)

You can use options at the top-right of the page:
* *Edit* - Edit your game's details.
* *Delete* - Delete your game and send it to the Recycle Bin.


  * ![](/img/fa/heart.png) - Set this game as your favorite. Each time you enter the portal the current game will shown without you having to select it.
  * ![](/img/fa/lock.png) - View your Games Access Secrets.
  * ![](/img/fa/globe.png) - Edit the Geo Restrictions for the game.
  * ![](/img/fa/edit.png) - Edit the top level information regarding your game.
  * ![](/img/fa/trash.png) - Delete this game.


## Editing Top-Level Game Information

*1.* To edit your game's details, click *Edit*:

![](img/GameOverview/8.png)

* On the *Game Details* tab, you can edit the following:

  * *Name* \- The name of your game, used to identify the game in the portal if you have several games
  * *Description* \- A description of the game
  * *Signup Bonuses* \- The amount of each of the currencies to award a new player when a new account is created
  * *Segment Configuration* - Configure Segments for your game. For more details, see [Segments](/Documentation/Configurator/Segments.md).

![](img/GameOverview/9.png)

* On the *Features & Integrations* tab, you can set up what your want to use in your game:
  * *Platform Features* - Select the GameSparks features you want to enable.
  * *Integrations* - Select the 3rd party providers you want to integrate with.

![](img/GameOverview/10.png)

* On the *Geographical Setup* tab, you can configure for the geographical distribution of your game:
  * *Primary Region* - Select the geographical region where your game will be published.
  * *Geo Restrictions* - Etc Etc.


## Snapshots

![](img/GameOverview/6.png)

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

## User Management

This area allows the creation of game Collaborators and Groups, these will be people that can log in with their user and view/edit the game, depending on the security settings set for them. An in-depth tutorial can be found [here](/Tutorials/Capabilities/README.md).
