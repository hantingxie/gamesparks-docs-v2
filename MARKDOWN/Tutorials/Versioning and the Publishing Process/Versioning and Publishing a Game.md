---
nav_sort: 1
src: /Tutorials/Versioning and the Publishing Process/Versioning and Publishing a Game.md
---

# Versioning and Publishing

## Versioning

You can create versions of your game configuration whenever you like. There are a number of reasons you might want to create a version, including:

  * You'll need to create a version when you publish your game to the live servers.
  * You've just finished a feature and the game is working exactly as you like. You're moving on to something new but want to be able to fall back on the existing configuration in case anything goes wrong.
  * You want to maintain a couple of configurations and publish them at different times (e.g. you have a weekend configuration of the game with 'weekend offer' prices).

You create a version by taking a 'snapshot' of the configuration. The process collects all your configuration information and stores it into a configuration set. This set also contains any data you have in your metadata collections. To create a snapshot, go to Configurator/Overview and click the plus icon in the Snapshots section.

![](img/Versioning/1.jpg)

You'll then be prompted to give a description to your snapshot. Choose something meaningful so you will be able to identify it in future when you may have several available.

![](img/Versioning/2.png)

Once you've saved the snapshot it's available in the Snapshots list in Configurator/Overview.

![](img/Versioning/3.jpg)

From here you can perform the following actions (by clicking on the icons to the right of the description):

  * *Copy* \- copies the snapshot and then you can choose to either use it to overwrite an existing game or create a new one (which will appear in the top left drop-down). If you are overwriting there is a fail-safe - a snapshot of the previous version is automatically created (called "AUTOSAVE - Pre Copy") which can then be deleted if all is in order.
  * *Delete* \- this will delete the snapshot
  * *Publish* \- this will take the snapshot and publish the configuration to the live servers. The snapshot that is currently published is highlighted in green. See below for more detail on publishing.
  * *Revert* \- updates your workspace with the snapshot version. There is a fail-safe - a snapshot of the previous version is automatically taken (called "AUTOSAVE - Pre Revert") which can then be deleted if all is in order.
  * *Preview* \- allows previewing any of the Snapshots without having to revert to them, editing will be disabled when previewing.

### Mongo Database Collections for Snapshots

When you take a Snapshot, the platform records all of your game's configuration into a configuration set:
  * This *includes* all Metadata Collections and their content.
  * This *excludes* all Runtime and System Collections and their content. These are created new for the Live stage when you *first publish* a game Snapshot and remain untouched when future Snapshots are published.


## Publishing

Once you have configured and tested your game, you will want to make it available to the public! The testing you have done to this point has been on the preview servers. These servers allow you to develop your game but are not suitable for use by a significant number of players - there is a limit of 100 concurrent connections per game.

<q>**Note:** You should not launch your game using the preview servers because player devices will not be able to connect when concurrency limits are reached.</q>

When you are ready to launch your game you need to save the configuration in a snapshot and then publish it to the live servers. These are designed for massive concurrency and can handle the loads generated when hundreds of thousands of players are using the game at the same time.

<q>**Going Live Checklist!** Before you attempt to create a Snapshot of your game and publish it to Live, please review the [Going Live Checklist](/Getting Started/Going Live Checklist/README.md) to ensure everything runs smoothly.</q>
