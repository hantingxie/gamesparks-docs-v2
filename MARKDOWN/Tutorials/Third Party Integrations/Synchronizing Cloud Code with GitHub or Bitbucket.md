---
nav_sort: 2
src: /Tutorials/Third Party Integrations/Synchronizing Cloud Code with GitHub or Bitbucket.md
---

# GitHub or Bitbucket Synchronization with Cloud Code Import / Export

If you're using GitHub or Bitbucket for your repositories, Good News! It's possible to synchronize your Cloud Code with GitHub or Bitbucket via the Import/Export features available in the platform.

In this tutorial, we assume that you already know what [GitHub](http://www.github.com) or [Bitbucket](https://bitbucket.org/dashboard/overview) are and that you have either a GitHub or Bitbucket repository already created.

<q>**GitHub Synchronization for Cloud Code** In this tutorial, we show you how to synchronize with GitHub to import/export your game's Cloud Code. The process for synchronizing with your Bitbucket repositories is essentially the same.</q>

![](img/GitSynch/14.png)

## Exporting Cloud Code

The first thing we can do is export our Cloud Code to our local machine.

 *1.* In your game, navigate to *Cloud Code* and select the *Export* button at the bottom of the *Scripts* section.

 ![](img/GitSynch/15.png)

 The entire Cloud Code for the game will be downloaded as a *.zip* file to your local machine.

 The contents of the .zip archive is structured on folders which resemble the categories as seen in the Portal's *Cloud Code* section. The contents of the .zip can look something like this:

![](img/GitSynch/20.png)


You will only see the directories in which you have created Cloud Code for. For example, if you only have code for *Events*, *User Messages*, and *Modules*, you'll only be able to see those directories in your export.

In each directory where Cloud Code exists, you will see a JavaScript (.js) file for every Cloud Code Event, Message, or Module:

![](img/GitSynch/21.png)

This is the exported Cloud Code and it's structural layout.

*2.* Navigate back to the *Game Overview* page and click to *Create* a Snapshot of the existing game.

*3.* Click to copy ![](/img/icons/copyicon.png) the Snapshot:

![](img/GitSynch/16.png)

A *Copy Snapshot* dialog appears:

![](img/GitSynch/19.png)

* Make sure you select to include the game configuration so that we can retain the corresponding Events and Cloud Code that was created for the source game.
* You can select to copy:
  * Over an existing game - the game configuration of the Snapshot will be copied over the existing game's configuration.
  * To a *New Game* - a new game will be created using the saved Snapshot configuration and the new game will be named using the convention: *COPY- << name of current game >>*.

*4.* Click *Copy*. When the Snapshot copy process has successfully completed, you'll get a message you can click the *View game* hotlink to be taken straight to the new game you have created:

![](img/GitSynch/17.png)

## Merging Cloud Code into a GitHub Repository

In the following steps, some type of versioning control application will be useful in adding the Cloud Code to your choice of repository.

*1.* Extract the contents of the .zip archive into the local working directory that is the path of your GitHub repository.

*2.* Make changes to the overall collection of Cloud Code files you exported earlier:
* Edit some of the Cloud Code in the .js files with an IDE or text editor.
* You can also delete some of the .js files from the local machine.

*3.* Commit and push the changes that include the exported Cloud Code into the remote repository.

*4.* Navigate to your project on [GitHub](http://www.github.com). You will notice that the Cloud Code changes have been successfully pushed to your remote repository.

 ![](img/GitSynch/22.png)

## Importing Cloud Code

*1.* In the Portal, go to the *Cloud Code* section and select *GitHub Import*:

![](img/GitSynch/14.png)

The GitHub Import page opens where you can connect the GameSparks platform to your GitHub account:

![](img/GitSynch/37.png)

*2.* Click to *connect your account*. A new browser tab is opened where you'll be required to log in again. When you've logged in, you're taken to your *Account Management* page:

![](img/GitSynch/38.png)

*3.* Under *Integrations*, click the red *Connect GitHub* button. A GitHub *Sign in* page opens:

![](img/GitSynch/39.png)

*4.* Enter your GitHub password and click *Sign in*. You are taken to an *Authorize application* page:

![](img/GitSynch/40.png)

*5.* Click to *Authorize application*. This will allow the GameSparks platform to link to your GitHub account.
* You might have to confirm you GitHub account password:

![](img/GitSynch/26.png)

When the connection completes, you're taken back to your *Account Management* page where you'll see that the GitHub button has changed to green:

![](img/GitSynch/41.png)

* You can use this to disconnect the platform from your GitHub account at any time.

Now that the platform is connected to your GitHub account, you'll be able to select your data from your GitHub account repositories.

*6.* Navigate back to the tab for the *GitHub Import* page and click the *Refresh* button. When the page refreshes, all of the repositories for your GitHub account are listed:

![](img/GitSynch/29.png)

* You can now follow a 4-step process to pull Cloud Code changes you want from your GitHub repositories into your game configuration.

*7.* **Step 1:** Select the repository from which you want import. The page shows the commits to the selected repository:

![](img/GitSynch/30.png)

*8.* **Step 2:** Select the commit you want to import from. The commit is loaded:

![](img/GitSynch/31.png)

* You'll see that the directory structure from the commit is replicated

*9.* **Step 3:** Select the **root directory**. The changes are loaded for ALL directories:

![](img/GitSynch/32.png)

<q>**Select ROOT Directory!** Although the directory structure is shown, you must select the root directory.</q>

*10.* **Step 4:** Select the changes you want to import. You can scroll down to inspect the changes made to Cloud Code in all directories and decide which changes you want to import:

* Any *ADDED* Cloud Code is shown in green:

![](img/GitSynch/33.png)

* Any *DELETED* Cloud Code is shown in red:

![](img/GitSynch/34.png)

* For any edited and *CHANGED* Cloud Code, the location of the editing change is identified and the before/after Cloud Code is shown:

![](img/GitSynch/35.png)

<q>**All Changes Selected!** All Cloud Code changes are selected by default for import - unselect the check box for any changes that you don't want import.</q>

*11.* If you want to create a Snapshot of your game before you import the Cloud Code changes, select the *Create Game Snapshot* at the bottom of the page:

![](img/GitSynch/36.png)

* Creating a Snapshot before importing Cloud Code changes from your Git repository will allow you to revert to the current game configuration, should anything go wrong after you import the changes.

*12.* Click *Import* to import the selected Cloud Code changes.
* When the import process has successfully completed, you'll see a message.
