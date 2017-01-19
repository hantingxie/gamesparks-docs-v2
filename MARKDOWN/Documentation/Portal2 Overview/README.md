---
nav_sort: 1
src: /Documentation/Portal2 Overview/README.md
---

# Portal2 Overview

Portal2 ushers in a new and exciting era for the GameSparks platform. As well as a redesigned user interface delivering smoother workflows and enhanced configurability, we've made some important functional changes to the original portal.

You can use this GameSparks Learn site to understand and explore Portal 2 in detail, but, before you head in, this page offers a overview of the new user interface as well as highlighting the functional changes brought in with Portal2.

## Portal2 User Interface

Here's some key points about the new UI design:

* **Main Navigation** - The main portal navigation been preserved and left-hand navigation consciously echoes the original portal.
* **Design Principles**
  * **Single Page Design** - A "single-page" UI design schema has been adopted with common layout patterns, resulting in a much smoother and easier workflows when performing common configuration tasks.
  * **Consistency of User Experience** - Standardized visual cues and affordances have been adopted, like red buttons for destructive actions, green for create actions, all providing a more accessible and intuitive interactive experience.
* **Alternative Themes** - You can quickly switch between a *Dark* or *Light* UI theme to suit your working preference.
* **Segmentation Enhanced** - This key feature now presents much more strongly and clearly within configuration objects across the UI, becoming much more accessible and easier to understand.
* **Game Management** - The Game Overview page has been given a properly independent status and re-worked to give improved workflows for game management tasks.
* **Experiments** - This extremely powerful feature has been promoted to its own top-level area and the main workflow unpacked into an intuitive 4-stage configuration wizard.


## Portal2 Functional Changes

Here's a list of the main functional changes from the original portal:

### Credentials

#### LogEventRequests and LogChallengeEventRequests:
* Toggle All has been removed and that function is carried simply by the main Request toggling all the secondary requests.

#### Player Credentials
* Player Credentials can now be edited for enabling and saving Admin Requests. Admin Requests can be activated on player Credentials.

### Properties
* These can no longer be saved without a value.

### Game Management
* Added the ability to select what Platform Features and Integrations you want for a Game.
* We no longer create default Groups for permissions. You also cannot rename a Group.
* Group Permissions for Games between the OLD and NEW portal will not be kept in synch:
  * For Groups in existing games, up to the point where a user opens a Group in Portal2 and edits and saves the permissions, they will agree. After the Save, the permissions will not agree—the save will not happen in the old portal.
  * To ensure permissions remain the same on both the old portal and Portal2, users must change and save in both (either way).

### Test Harness
* Now allows users to select which Credential they want to use.

### Cloud Code
* Bitbucket integration for importing Cloud Code has been added.
* The Cloud Code History Tool works in similar way to the old portal but with an important difference:
  * When a Snapshot is selected in the *Base* drop-down, no initial filtering is done to remove any “No-Cloud-Code-Difference” Snapshots from the *Compare To* drop-down.

### Segmentation
* While the Segmentation itself has not functionally changed, configuring it is more straightforward.
* Segmentation for individual fields can be done directly.

### Messages
* The *Include in Push Count* switch has been removed, since this wasn’t used.

### Running Totals
* The way the naming reference for Running Totals is built up has changed. For example:
  * For an Achievement triggered by Leaderboard set up. When you select a Leaderboard for triggering when the Achievement will be earned, you can then select a Trigger or Triggers from what has been set on the Leaderboard as Running Totals. This Trigger is NOW named as two-value Leaderboard Short Code/Event Attribute Short Code selected as a Running Total on that Leaderboard.
  * PREVIOUSLY, this naming reference or address was built up using simply the Running Total = Event/Attribute name.
  * In addition, the reference now includes a suffix for the Running Total filter, such as “all” for “all values”, “gt” for “greater than”, and so on.
* THIS ONE affects new REST API

### REST API
* GENERAL warnings for those people simply working through REST API, that is, they do their game configuration elsewhere then use GameSparks through REST!

### API Stream Analytics
* A new API Stream Analytics page has been added, which you can use to make direct queries against requests and message API calls stream and then display results into three chart formats without having to first create a chart to carry and deploy the query.
