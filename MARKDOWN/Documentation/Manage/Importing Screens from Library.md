---
nav_sort: 2
src: /Documentation/Manage/Importing Screens from Library.md
---

# Importing Screens from Library

The Gamesparks platform offers several pre-built management Screens, which you can import from a Screen library into your game. The Screens are designed to help you perform your core game management tasks:
* Player Management
* Leaderboard Management
* Script Log Viewer

These Screens have been built with ease of use and convenience very much in mind:
* User friendly, customizable, and provide you with very useful ways of visually searching for, accessing, and editing records.
* When you import a Screen, its constituent Snippets are imported along with it as a package.
* Working with the Screens requires no code-writing skills or ability to access and work with the NoSQL database, which means your non-dev team members can easily set-up and use them.

This topic shows you how to download any of the pre-configured Screens and introduces you to the functionality each Screen offers.

<q>**Player Profile Screen!** For a detailed account of importing and building a Player Profile Screen, check out this tutorial.</q>

## Importing a Pre-Built Screen

*1.* Go to *Manage>Admin Screens*. The *Manage* page opens.

*2.* Click *Import from Library*:

![](img/ImportScreens/1.png)

The *Import from Library* page opens.

*3.* Click the *Import* drop-down and select the Screens you want to import:

![](img/ImportScreens/2.png)

Here, we've selected to import the *Player Management* and *Leaderboard Management* Screens.

*4.* Click *Import*. When the import completes, you are taken back to the *Manage* page:

![](img/ImportScreens/3.png)

* The imported Screens are added to the *Screen Builder*.
* A Screens Snapshot has been automatically taken to safeguard any existing Screens configuration - if you had already created Screens with the same Short Codes as any imported Screens, these existing Screens will have been overwritten. You can revert to the Screen Snapshot at any time.

*5.* Select the *Snippets* tab:

![](img/ImportScreens/4.png)

* You'll see that fourteen new Snippets have also been imported for the *Player Management* and *Leaderboard Management* Screens.
* If you import the *Script Log Viewer* screen, three Snippets will also be imported for this Screen.

*6.* Select the *Charts* tab:

![](img/ImportScreens/5.png)

* You'll see the a new *total_requests* Chart also been imported for the *Player Management* Screen.

## The Screens

When you have imported a Screen from the library, you'll see it available for selection from the *Manage* menu:

![](img/ImportScreens/6.png)

Imported library Screens and their supportive Snippets and Charts are designed for common game management and monitoring tasks and this section introduces each of the screens. You can also modify and extend imported Screens, Snippets, and Charts to suit your own specific requirements - see [Working with Dynamic Forms](/Documentation/Manage/Working with Dynamic Forms.md).

### Player Management

The *Player Management* Screen lets you build a search query for players and then bring up a Screen to show details of a player's profile for reviewing and editing.

*1.* Open the *Player Management* Screen, build a player search query and click *Submit*.

![](img/ImportScreens/7.png)

The players that satisfy your search query criteria are returned:

![](img/ImportScreens/8.png)

*2.* Click to view and edit ![](/img/fa/edit.png) a player's details. An *Edit Player* Screen appears where you can review and edit various aspects of the player's profile.

<q>**More on this Screen?** For a fuller account of working with the *Player Management* Screen, see the [Player Profile Screen](/Tutorials/Analytics, Segmentation and Game Management/Creating a Player Profile Screen.md) tutorial.</q>

### Leaderboard Management

The *Leaderboard Management* Screen allows you to view the Leaderboards in your game and review the ranking and entries on each Leaderboard.

*1.* Open the *Leaderboard Management* Screen. The Leaderboards are listed:

![](img/ImportScreens/9.png)

In this game, note that we have two partitioned Leaderboards which we can click to expand and use a drop-down to select for each partition - *Level Leaderboard* and *Scheduled Leaderboard*.

*2.* Click to view and edit ![](/img/fa/edit.png) a Leaderboard:

![](img/ImportScreens/10.png)

You can:
* Review the details for each entry on the Leaderboard.
* Enter a rank value and click to *Go To Rank*.
* Enter a player or Team ID and click *Go to Entry*.
* Delete individual entries.
* Click to *Delete All Entries*.


### Script Log Viewer

You can use the *Script Log Viewer* Screen to search for and review the logs for your game.

<q>**Logging for Games?** For more details about logging, see [SparkLog](/API Documentation/Cloud Code API/Utilities/SparkLog.md).</q>

*1.* Open the *Script Log Viewer* Screen and build a log search query:

![](img/ImportScreens/11.png)

* You can click to *Edit logging level*.

In this example, our query searches for log entries at the *Debug* level against the *ChallengeStartedMessage* script.

*2.* Click *Submit*. The log entries for your game that satisfy the search query criteria are returned:

![](img/ImportScreens/12.png)
