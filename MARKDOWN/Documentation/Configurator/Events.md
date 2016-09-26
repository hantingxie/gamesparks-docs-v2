---
nav_sort: 3
src: /Documentation/Configurator/Events.md

---

# Events

You can use Events to define custom data structures that you want to pass into the platform via the [LogEventRequest](/API Documentation/Request API/Player/LogEventRequest.md) and [LogChallengeEventRequest](/API Documentation/Request API/Multiplayer/LogChallengeEventRequest.md) API calls.

## Managing Event Configurations

The Configurator *Events* page lists Events and allows you to create new Events and edit or delete existing ones.

![](img/Events/1.jpg)

You can use icon button options (highlighted above):

  * ![](/img/fa/plus.png) - Add a new Event.
  * ![](/img/fa/edit.png) - Edit Event.
  * ![](/img/fa/trash.png) - Delete Event.

## Creating a new Event Configuration

![](img/Events/2.jpg)

The Create/Edit screen contains the following fields:

  * *Name* \- Name of the Event, which is used to identify the game in the portal if you have a number of Events.
  * *Description* \- Description for the Event.
  * *Short Code* - Short Code of the event, which is used by the API to allow you to identify which event you want to call.

### Creating Event Attributes

Each Event can have a number of attributes associated with it.

![](img/Events/3.jpg)

Add an attribute by clicking the ![](/img/fa/plus.png) icon.  Each attribute has a number of different configuration options that can be defined within the form:

  * *Name* \- Name of the Attribute, which is used to identify the attribute if there are several associated with an Event.
  * *Short Code* \- Short Code of the Attribute, which is used by the API to allow you to identify which Attribute you are trying to set.
  * *Data Type* \- Each attribute needs to be defined as either String, Number or JSON.
  * *Default Value* \- Allows a specific value to be used if the user request does not contain this attribute.
  * *Default Calculation* \- Select the calculation you want to use for when the Event/Attribute is used as a running total a Leaderboard. Select *Used In Script* if you do not want to make the Event/Attribute available for a Leaderboard running total:
    * *Maximum* \- A running total will be created to track the maximum value posted.
    * *Minimum* \- A running total will be created to track the minimum value posted.
    * *Sum* \- A running total will be created to add all the values posted together.
    * *Count* \- A running total will be created to count the number of times the player has called the event.
    * *Last* \- A running total will be created using the last value posted.
    * *Used In Script* \- The Event will not be used in a running total.
    * *Grouped* \- The running total will use this attribute to group other attributes. This will lead to a running total with an entry per attribute/user combination.
    * *Supplemental* \- A running total will be created with no value calculated. You can use this when you want to store some extra information within the game context but do not want this to affect on the Leaderboard ranking. (For example, in a racing game you can keep note of weather conditions on the track as well as player lap times but changing weather conditions do not affect the player's Leaderboard ranking.)

<q>**Attributes for Leaderboard Running Totals!** Any Event that you create with at least one Attribute where you select any *Default Calc* for the Attribute *except Used in Script* means that the Event will be available for selection as a running total when you create and configure Leaderboards for your game. [Running Totals](/Documentation/Configurator/Running Totals.md) is further explained in the next page.</q>
