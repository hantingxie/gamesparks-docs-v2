---
nav_sort: 1
src: /Documentation/Portal2 Overview/README.md
---

# Portal2 Overview

Portal2 ushers in a new and exciting era for the GameSparks platform. As well as a redesigned user interface delivering smoother workflows and enhanced configurability, we've made some important functional changes to the original portal.

You can use this GameSparks Learn site to understand and explore Portal 2 in detail. But before you head in, this page offers an overview of the new user interface as well as highlighting the functional changes brought in with Portal2.

## Portal2 User Interface

Here's some key points to note for the new UI design:

* **Game Creation** - This has been very effectively streamlined using a 3-stage set up wizard where you can now select just those platform features and 3rd party integrations you want for your game.
* **Main Navigation** - The main portal navigation is preserved and the left-hand navigation consciously echoes the original portal.
* **Design Principles**
  * **Single Page Design** - A "single-page" UI design schema has been adopted across the portal with common page layout, resulting in smoother workflows when performing your configuration tasks.
  * **Consistency of User Experience** - Standardized visual cues and affordances have been adopted, like red buttons for destructive actions, green for create actions, all contributing to a more intuitive interactive experience.
* **Alternative Themes** - You can quickly switch between a *Dark* or *Light* UI theme to suit your working preference.
* **Segmentation Enhanced** - This key feature now presents much more strongly and clearly within configuration objects across the UI, making it much more accessible and easier to understand.
* **Game Management** - The Game Overview page has been re-worked to give improved workflows for all your game management tasks.
* **Experiments** - This extremely powerful feature has been promoted to its own top-level area and the main workflow unpacked into an intuitive configuration wizard.
* **NoSQL Explorer** - You can now open multiple Mongo DB Collections tabs and query and work with several Collections at the same time.


## Portal2 Functional Changes

Here's a list of the main functional changes from the original portal:

### Credentials

#### Player Credentials
* Player [Credentials](/Documentation/Configurator/Credentials.md) can now be edited for Admin Requests, meaning Admin Requests can now be activated for this type of Credential.

#### LogEventRequests and LogChallengeEventRequests:
* *Toggle All* has been removed and that function is now carried by the main Request toggling all the secondary requests.

### Properties
* [Properties](/Documentation/Configurator/Properties.md) can no longer be saved without a value.

### Game Management
* From [Game Overview](/Documentation/Game Overview/README.md), you now have the ability to select what Platform Features and Integrations you want for a Game.
* We no longer create default Groups for permissions.
* You cannot rename a Group.
* Group Permissions for Games between the old portal and Portal2 will not be synchronized:
  * For Groups in existing games: up to the point where a user opens a Group in Portal2 and edits and saves the permissions, they will agree. After the Save, the permissions will not agree — the save will not happen in the old portal.
  * To ensure permissions remain the same on both the old portal and Portal2, you must change and save in both (either way).

### Integrations

* Firebase Cloud Messaging (FCM) is now supported in the portal, allowing push notifications to be sent to Android and iOS devices. With Firebase, players will receive these notifications even if a game is backgrounded on their device.

### Test Harness
* You can now select which Credential you want to use when working in the [Test Harness](/Documentation/Test Harness/README.md).

### Cloud Code
* Bitbucket integration for importing [Cloud Code](/Documentation/Configurator/Cloud Code.md) has been added.
* The Cloud Code History Tool works in similar way to the old portal but with an important difference:
  * When a Snapshot is selected in the *Base* drop-down, no initial filtering is done to remove any “No-Cloud-Code-Difference” Snapshots from the *Compare To* drop-down.

### Segmentation
* While the [Segmentation](/Documentation/Configurator/Segments.md) itself has not functionally changed, configuring it is more straightforward.
* Segmentation for individual fields can be done directly.

### Messages
* The *Include in Push Count* switch has been removed from [Message](/Documentation/Configurator/Messages.md) configuration, since this wasn’t used.

### Running Totals
* The way the naming reference for [Running Totals](/Documentation/Configurator/Leaderboards/Running Totals.md) is built up has been changed to help clarify just which Running Total it is:
  * For example, take the case of an Achievement triggered by a Leaderboard set up. When you select a Leaderboard for triggering when the Achievement will be earned, you can then select a Trigger or Triggers from what has been set on the Leaderboard as Running Totals. This name of a Trigger is now a two-value composite: the Leaderboard Short Code combined with the Event Attribute Short Code which has been selected as a Running Total on that Leaderboard.
  * Previously, this naming reference or address was built up using simply the Running Total = Event/Attribute name.
  * In addition, the reference now includes a suffix for the Running Total filter, such as “all” for “all values”, “gt” for “greater than”, and so on.

### REST API
* There's been some general REST API improvements and you can check out the documentation for these [here](/API Documentation/REST APIs/README.md).

<q>**Upgrading your REST APIs!** There is a new REST API and you must upgrade to this as soon as possible. For details of how to do this, see [here](/Documentation/Upgrading REST APIs/README.md). </q>

### API Stream Analytics
* We've added a new [API Stream Analytics](/Documentation/Analytics/API Stream Analytics.md) page, which you can use to make direct queries against the current requests and message API calls stream and then display your query results into three chart formats. This saves you having to first create a chart to carry and deploy the query.

### Manage
* The pre-built *Player*, *Leaderboard*, and *Script* Log management screens are no longer imported into the [Manage](/Documentation/Manage/README.md) section by default for each new game. However, you can now quickly import these from the Screens Library, as and when you need them for your game management.
* The Import/Export for Screens, Snippets, and Queries has been removed. Instead, you can now copy a saved Screen Snapshot directly to another game.

### Experiments and Charts
* You can now build a query for an Experiment or Chart using types that are not currently being used in the runtime server.
