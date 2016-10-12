---
nav_sort: 3
src: /Documentation/Configurator/Teams.md
---

# Teams

The Teams functionality on the GameSparks platform allows you to define different team types for grouping players:
* **Team Types.** You can create a number of different Team types with different rules and these rules are respected when using the team-based API Methods:
    * Once you have Teams in place, you can use them for all social requests as well as for team-based Leaderboards (where there is an entry for each Team, rather than an entry for each player).
    * Team instances can be created by your players and will comply with the Team type configuration settings. A tutorial on setting up teams for chat is available [here](/Tutorials/Social Features/Setting Up Chat Messages.md).
* **Team Achievements.** A Team can earn achievements in the same way that a player can. When a Team earns an achievement, each Team member without the achievement is given the award defined against it.

## Managing your Teams

![](img/Teams/3.png)

The *Teams* page lists the team types you have configured in the platform. You can use the following options (highlighted above):

  * *Add* - Add a new Team.
  * ![](/img/icons/editicon.png) - Edit Team.
  * ![](/img/icons/deleteicon.png) - Delete Team.

## Creating a Team Type Configuration

Click to *Add* a new Team type. The page adjusts:

![](img/Teams/4.png)

Enter the details for your new Team type:

  * *Short Code* \- Short Code for the Team, to be use by API methods. Short Codes are always unique.
  * *Name* \- Name of the Team (Used within the portal only for identification).
  * *Social* \- Team members will be regarded as friends of the friends of the owner.
  * *Extended Social* \- Team members will be regarded as friends with each other.
  * *Max Members* \- Maximum number of players that can be in a Team of this type.
  * *Max Membership Per User* \- Maximum number of this Team type a player can be in (Set to 0 for unbounded).
  * *Max Ownership Per User* \- The maximum number of this Team type a player can own (Set to 0 for unbounded).
