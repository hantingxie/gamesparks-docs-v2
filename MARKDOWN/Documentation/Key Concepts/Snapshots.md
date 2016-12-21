---
nav_sort: 5
src: /Documentation/Key Concepts/Snapshots.md
---

# Snapshots

The Snapshots feature allows you to *Create*, *Copy*, *Delete*, *Publish*, *Revert* and *Preview* the configuration of your Game, allowing for in-depth management of each stage of the release.

<q>**Game Snapshots vs. Screen Snapshots!** Game Snapshots *do not contain* any of the Manage section configuration you've built up for your Admin Screens. You can create separate *Screen Snapshots* for the Manage configuration and publish these to the Live environment independently of your game Snapshots. For details, see [Creating and Managing Screen Snapshots](/Documentation/Manage/Creating and Managing Screen Snapshots.md).

## Snapshots: Creation and Basics

You can create a Snapshot of the current game configuration by clicking *Create* in the *Snapshots* section on the *Game Overview* page.

![](img/Snapshot/11.png)

A *Create Game Snapshot* dialog appears where you can enter a description of the Snapshot.

![](img/Snapshot/12.png)

Click *Create* to create the Snapshot:

![](img/Snapshot/14.png)

You can then use icon button options (highlighted):

  * ![](img/Snapshot/copyicon.png) - Copies the Snapshot to create a new or overwrite an existing game. You can only overwrite a game if you are a game owner or admin for the game. You'll have the option to copy:
    * Only the metadata from the original Snapshot.
    * Only the game configuration.
    * Both the metadata and the game configuration.
    * Downloadables
    * Collaborators

<q>**Important!** Don't worry about overwriting the target game's configuration. There is a fail-safe - a Snapshot of the target game's previous version is automatically created (called "AUTOSAVE - Pre Copy") before the copy occurs.</q>
  * ![](img/Snapshot/deleteicon.png) - Deletes the Snapshot.
  * ![](img/Snapshot/publishicon.png) - Publish the configuration to the LIVE servers. The snapshot that is currently published is highlighted in green. See below for more detail on publishing.
  * ![](img/Snapshot/reverticon.png) - Revert your workspace with the selected Snapshot version. There is another fail-safe - a Snapshot of the previous version is automatically taken (called "AUTOSAVE - Pre Revert").
  * ![](img/Snapshot/previewicon.png) - Preview any of the Snapshots without having to revert to them, editing will be disabled when previewing.

### Mongo Database Collections for Snapshots

When you take a Snapshot, the platform records all of your game's configuration into a configuration set:
  * This *includes* all Metadata Collections and their content.
  * This *excludes* all Runtime and System Collections and their content. These are created new for the Live stage when you *first publish* a game Snapshot and remain untouched when future Snapshots are published.

## Copying a Snapshot

![](img/Snapshot/15.png)

The *Copy Snapshot* dialog gives you options for customizing your copy:

  * *Game* \- from the drop-down, you can choose to copy the Snapshot to a new game or to overwrite an existing game that you have access and permissions to edit.
  * *Include metadata collections* \- choose whether to include the metadata for the copy of the game.
  * *Include game configuration* \- choose whether to copy the game configuration onto an existing game, overwriting any existing configuration. When copying to a new game, this option is disabled because in this case the Snapshot's game configuration is always copied.
  * *Include downloadables* - choose whether to copy the binary data content you have uploaded to the game.
  * *Include collaborators* - choose whether to copy the game's collaborators.

## Deleting a Snapshot

When you select delete, a warning/confirmation dialog appears. Press *Ok* to confirm *only if you are absolutely sure* you want to delete the Snapshot.

![](img/Snapshot/16.png)

## Publishing a Snapshot

Publishing a Snapshot places the configuration of the game into the LIVE environment, where the game can then be accessed by your players. For in-depth tutorial on versioning read [here](/Tutorials/Versioning and the Publishing Process/Versioning and Publishing a Game.md).

![](img/Snapshot/17.png)

Once you confirm your selection to publish the Snapshot, it will be highlighted in green within the list of Snapshots:

![](img/Snapshot/18.png)

<q>**Going Live Checklist!** Before you publish your Snapshot to Live, please review the [Going Live Checklist](/Getting Started/Going Live Checklist/README.md) to ensure everything runs smoothly.</q>

## Reverting a Snapshot

You might want to revert to earlier version of your game configuration or saved metadata collections if you have accidentally removed some configuration details or if something recently went wrong. When Reverting to a Snapshot you'll be prompted for a confirmation.

![](img/Snapshot/19.png)

<q>**Snapshot AUTOSAVE!** When you revert a Snapshot, your current configuration is saved to create an automatic Snapshot of everything as it was before the revert:</q>

![](img/Snapshot/20.png)

## Previewing a Snapshot

You can preview a Snapshot and inspect the game configuration of that Snapshot, which saves you having to fully revert to it then having to revert back to your original state. In Snapshot Preview mode, all editing is disabled and you'll see what's being previewed at the top of the page:

![](img/Snapshot/21.png)

* The Snapshot Preview header tells you what Snapshot you are currently previewing, when it was created, whether it is live or not, and who it was created by.
* To exit the Snapshot preview, click *Exit Preview*.
