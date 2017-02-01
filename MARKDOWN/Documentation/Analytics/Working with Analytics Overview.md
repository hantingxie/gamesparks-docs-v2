---
nav_sort: 1
src: /Documentation/Analytics/Working with Analytics Overview.md
---

# Working with Analytics Overview

## Introduction

The GameSparks platform aggregates a wide range of analytics data and provides you with key performance trends and metrics that track player interaction with your game:
* Most common reporting requirements for monitoring player interaction and engagement are covered.
* If you have any special needs for analytics reporting, you can build custom screens through the *Manage* section of the portal - see below *Customizing Analytics Reporting*.

The Configurator *Analytics Overview* page contains four tabs:
* **Overview**
  * Shows "Big Numbers" listing your game's key performance metrics.
  * Contains graphs tracking player engagement with your game.
* **Performance** - Contains performance-related graphs.
* **Custom** - Contains graphs for data gathered on usage of the *AnalyticsRequest* against the GameSparks platform.
* **Export** - Export analytics data collections as JSON.

<q>**UTC Time Zone.** All of the analytics graphs are set to Coordinated Universal Time (UTC).</q>

## Overview Tab

![](img/Analytics/17.png)

There are several graphs on the *Overview* tab:

  * *New / Returning players* - Shows the number of new (in blue), returning players (in orange).
  * *Average Session Duration* - Shows the average session duration in seconds. Note that this chart is driven by *EndSessionRequest* submissions and will only build if some have been made.
  * *Retention % by day* - Shows the number of returning players as a percentage of the total players for a each day over the last 30 days.
  * *Average DAU / MAU* - Shows the average *Daily Active* player count over the *Monthly Active* player count. This is a measure of 'engagement'.
  * *Devices* - Shows the different devices that your players are using to play your game.
  * *Players by Country* - Shows the different countries where your game is being played.

<q>**Exporting Graph Data.** You can export the JSON data collections on which the graphs are based directly from each graph. See below [Exporting Analytics Data from Graphs](#Exporting Analytics Data from Graphs).</Q>

### Checking the Big Numbers

The *Big Numbers* are shown across the top of the *Overview* tab:

![](img/Analytics/18.png)

These numbers provide key aggregated analytics data metrics about how well your game is performing and indicates levels of engagement within the game’s current player base:

  * *Active Players (now)* - The total number of players that are currently connected to your game.
  * *DAUs (since midnight)* - The total number of unique Daily Active Players since midnight.
  * *Avg DAUs (last 30 days)* - A rolling average over the last 30 days for the DAU Big Number.
  * *MAUs (last month)* - The total number of active players for last month and the current month.
  * *MAUs (this month)* - The total number of active players for the current month.
  * *Average Session Duration (today)* - The average player session duration for today.

<q>**Live Data!** The Big Numbers show live data and are updated every minute or so.</q>

## Performance Tab

![](img/Analytics/19.png)

The *Performance* tab displays a number of performance-related graphs:

  * *Average Requests per Player* - Shows the average number of requests generated per player within your game.
  * *Average Response Time (ms)* - Shows the average response time (in milliseconds) that the GameSparks platform has taken to respond to API request calls.
  * *Average Javascript Execution Time (ms)* - Shows the average time (in milliseconds) that the GameSparks platform has spent executing your Cloud Code.
  * *Average Storage per Player (bytes)* - Shows the average amount of cloud data per player that your game is using.
  * *Average Bandwidth per Player (bytes)* - Shows the average amount of bandwidth per player that your game is using.

<q>**Per Player Spikes!** On the per player graphs, the average is calculated against the number of active players in that time period. This means that if your are using an hourly sampling frequency, these graphs can look skewed if a particular hour has only a relatively small number of active players compared to the number of active players in other hours.</q>

## Custom Tab

![](img/Analytics/27.png)

 The *Custom* tab contains graphs which show the data gathered as a result of your game sending an [AnalyticsRequest](/API Documentation/Request API/Analytics/AnalyticsRequest.md) to the GameSparks platform:

  * *Count* - Shows the number of times a given custom key has been sent via the *AnalyticsRequest*.
  * *Average per Player* - Shows the average number of times per player that a given custom key has been sent via the *AnalyticsRequest*.
  * *Average Duration* - Shows the average duration for each timed request sent via the *AnalyticsRequest*.

## Export Tab

You can export any of the JSON analytics data collections from the *Export* tab:

*1.* Use the drop-down on the *Collection* field to show the data collections menu:

![](img/Analytics/20.png)


*2.* Select the data collection you want and then click *Export*. A *Save/Open file* dialog appears and you can save or view the JSON text file.

<q>**Note:** You can export analytics data collections directly from graphs on the other tabs - see below *Exporting Analytics Data from Graphs*.</q>

## Working with Analytics Graphs

When you are viewing analytics graphs, you can use several options to adjust the data graph display and you can export data directly from graphs.

### Using Display Control Menus

![](img/Analytics/21.png)

Use the two drop-down menus at top-right to control the data displayed in the analytics graphs.

  * *Date Range* - Select from a defined date range or select specific start and end dates for the data set displayed:

  ![](img/Analytics/22.png)

  * *Sample frequency* - Select between hourly, daily, and monthly frequencies:

  ![](img/Analytics/23.png)

### Switching between Preview and Live

You can use the *Preview/Live* switch at the top of the page to select which stage analytics data are displayed for:
* Preview:

  ![](img/Analytics/24.png)

* Live:

  ![](img/Analytics/24A.png)


### Exporting Analytics Data from Graphs

You can export the analytics data collection on which any of the analytics graphs are based as a JSON file:
* Click the *Export as JSON* button at the top-right of the graph canvas

![](img/Analytics/25.png)

A *Save/Open file* dialog appears and you can save or view the JSON text file.

### Toggling Stacked Charts

Analytics graphs that track more than one metric can be difficult to read:
* You can click to *Toggle Stacked Charts* and view these multi-measure graphs in a more accessible stacked format:

![](img/Analytics/26.png)

### Toggling Chart Legends

If a chart contains many data sets, the legend below the chart can become cluttered and might prevent the chart rendering correctly. For example, if your game has players located in many countries worldwide, the legend on the *Players by Country* chart on Overview, might become cluttered:
* If a chart has more that 20 data sets, the legend below the chart is automatically toggled off.
* You can click to manually toggle a chart legend off and on:

![](img/Analytics/28.png)

* Here we've toggled off the legend on the Count chart on the Custom tab.

## Customizing Analytics Reporting

If you have any special needs for analytics reporting, you can build custom screens for querying the NoSQL database through the [Manage](/Documentation/Manage/README.md) section of the portal. From here, you can build ad hoc queries for analysis against raw request and response data.
