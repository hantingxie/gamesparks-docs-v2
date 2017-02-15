---
nav_sort: 13
src: /Documentation/Configurator/Segments.md
---

# Segments

## What are Segments?

Segments allow you to create partitions for different users and apply various rules to different areas of the platform. Segments offer you an extra dimension of flexibility for customizing player experience and behavior.

## Examples

Here's two example use cases where Segmentation comes in very useful:

*1.* Let's suppose I have an international blockbuster game with players connecting from different parts of the World. In order to offer a more personalized experience for my players, I might want to segment players by region or country. I can create a Segment based on country, with Segment Values of the countries my players are situated in. When added to such a Segment, the players will receive a different experience. For example, each Segment Value (country in this case) could have assign values for:
* Virtual Goods.
* The awards players receive upon obtaining an Achievement.
* The rates of 6 currencies that spread across their game.

*2.* What about language? A much simpler and customizable method than Geo Locations would be to introduce a language Segment. Based on the user's Segment Values for a language Segment, users could receive messages for new high scores, challenges, and team invitations all in their respective native languages, as well as customizing the name and descriptions of Leaderboards, Challenges, Achievements, and so on.

## Managing Segment Configurations

To create and edit Segments, go to *Configurator > Segments* and select the *Segments* tab. Existing Segments are listed:

![](img/Segments/7.png)

You can use the following options (highlighted above):

 * *Add* - Add a new Segment.
 * ![](/img/icons/editicon.png) - Edit Segment.
 * ![](/img/icons/deleteicon.png) - Delete Segment.

## Creating a Segment and Adding Segment Values

You can create and assign multiple segments, each with their own set of values.

*1.* On the *Segments* tab, click *Add*. The page adjusts:

![](img/Segments/8.png)

*2.* Enter the details of the new Segment:
* *Short Code* \- A mandatory field used to give the Segment a unique identifier for use elsewhere in the Portal and in Cloud Code.
* *Name* \- A mandatory field used as an identifier to help find the Segment in the Portal.
* *Description* \- A mandatory field which should be used to describe the Segment and explain its purpose.

*3.* To add values to the Segment, under *Values* click *Add*.

*4.* Enter a *Short Code*, *Name*, and *Description* for each Segment value that you add:

![](img/Segments/9.png)

In this example, we've added 6 Values to our *Country* Segment:
* We can now assign different Segment/Value pairs to the players of our game and on the basis of these segment assignments, differentiate player experience.

## Building Segment Queries

You can build *Segment Queries* to define rules which determine which player's are subjected to a specific segmentation of a configuration object in your game:
* For example, you might segment a Virtual Good into three segments and set different currency values for the Virtual Good for each segment. You can then use Segment Queries to determine which players experience which Virtual Good costs, depending on the Segment/Value pair a player has been assigned.

<<<<< Using Custom Queries >>>>>

### Setting Segment Query Filters

When you add the Segment Queries you want for segmenting you game's configuration objects, you can select just those filters you want to use when building your queries:

*1.* Go to *Configurator>Segments* and select the *Segments Queries* tab.

*2.* Click *Segment Query Filters*:

![](img/Segments/14.png)

The *Segment Query Filters* panel appears:

![](img/Segments/15.png)

*3.* Select the *Segment Query Filters* you want to use when building your Segment Query:
* The filters available will depend on your game's set up and the configuration objects created for your game. By default all are selected.
* Uncheck any filters you don't want to use when building your Segment Queries.
* In the current example, we've unchecked 4 Virtual Goods filters.

*4.* If you want to add custom filters for building your Segment Queries, click *Add*. Etc., Etc.

![](img/Segments/17.png)

*5.* Click to *Save* your *Segment Query Filters* selection.

### Adding Segment Queries

Now that we've selected our Segment Query Filters, here's how to build a couple of Segment Queries that we'll use [below](#Segmenting Configuration across the Portal) to segment an Achievement:

*1.* Go to *Configurator>Segments* and select the *Segment Queries* tab.

*2.* Click to *Add* a new query.

*3.* Enter the details of the new Segment Query:
* *Short Code* \- A mandatory field used to give the Segment Query a unique identifier for use elsewhere in the Portal and in Cloud Code.
* *Name* \- A mandatory field used as an identifier to help find the Segment Query in the Portal.
* *Description* \- A mandatory field which should be used to describe the Segment Query and explain its purpose.

*4.* Use the drop-downs to build the query you want:
* This can be a complex multi-group/multi-rule query using the *Add Group* and *Add Rule* buttons on the builder.
* For the current example, we've set up a single-rule query:

![](img/Segments/16.png)
* Here we've used the *Country* Segment to create a Segment Query - only players assigned the Segment/Value pairing *COUNTRY_SEG/JP_COUNTRY_SEGVAL* will be subject to the alternative values of that object we've set for a specific segment.

*5.* Click to *Save and Close* the new Segment Query.

*6.* Repeat the above steps to create a second Segment Query:

![](img/Segments/18.png)
* Here we've used the *Country* segment to create a Segment Query - only those players assigned the Segment/Value pairing *COUNTRY_SEG/PL_COUNTRY_SEGVAL* will be subject to the alternative values of that object we've set for a specific segment.

*7.* Click to *Save and Close* this second new Segment Query.

We now have two Segment Queries we can use when we segment configuration objects in our game and impose different experiences on players assigned different Segment/Value pairs.

## Setting Segments Using Cloud Code

Not all Segments have to be set through the Configurator. Segments and their Values can be set on-the-fly using [Cloud Code](/Documentation/Configurator/Cloud Code.md). For any Segment type, a player can have a single Value set, and you can set (or unset) these Values via Cloud Code using _SparkPlayer.setSegmentValue(TYPE, VALUE)_ or find the current Value of a Segment they have, using _myPlayer.getSegmentValue("TYPE")_.

![](img/Segments/13.png)

## Segmenting Configuration across the Portal

Within the portal, you can segment your configuration to set different parameters for different Segments. For example, you can have:
* A different price for a virtual good for a particular Segment.
* A different virtual good award and currency reward for an Achievement depending on the player's country Segment.

Here, we'll segment an Achievement using the two Segment Queries we built [above](#Adding Segment Queries).

*1.* Go to *Configurator>Achievement*.

*2.* Click to edit an Achievement you want to segment.

*3.* Click *Segment*. The *Segment Configuration* panel opens:

![](img/Segments/19.png)

*4.* Click *Add Segment*.

*5.* Enter the alternative values you want to use for the segmentable Achievement fields and which will be applied to players put into this Segment.

*7.* Use the drop-down to select the *Segment Query* you want to use to determine which players are put into this segment of the Achievement:

![](img/Segments/20.png)
* Here we've selected the *COUNTRY_SEG_QUERY_JP*. This means that only players assigned the *COUNTRY_SEG/JP_COUNTRY_SEGVAL* Segment/Value pair will be subject to the alternative values for this Achievement segment.  

*8.* Click *Add Segment* again and add a second segment for the Achievement:  

![](img/Segments/21.png)
* Here we've selected the *COUNTRY_SEG_QUERY_PL*. This means that only players assigned the *COUNTRY_SEG/PL_COUNTRY_SEGVAL* Segment/Value pair will be subject to the alternative values for this Achievement segment.

*9.* Click to *Save and Close* the Achievement segmentation.

### Ordering Segment Configuration

Segmented values within the portal can be ordered, where the order is used to find the most appropriate value for the current player. Simply click and hold on the *Reorder* icon and drag-and-drop a Segment to where you want it:

![](img/Segments/11.png)

## Social Integration with Segments

One of the most powerful features of Segmentation is that it allows for different segment types to be socially connected to different games or apps. For example, players of different nationalities or language preferences could have segments which would socially connect them to a different version of a developer's app or game on Facebook or Twitter:

![](img/Segments/12.png)
