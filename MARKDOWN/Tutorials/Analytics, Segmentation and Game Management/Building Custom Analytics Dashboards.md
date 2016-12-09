---
nav_sort: 1
src: /Tutorials/Analytics, Segmentation and Game Management/Building Custom Analytics Dashboards.md
---

# Building Custom Analytics Dashboards

Using Dynamic Forms you can quickly and easily build a Custom Analytics Dashboard that will have nearly limitless expandability and suit your personal needs. However, we strongly recommend that you read the [Dynamic Forms API](/API Documentation/Dynamic Forms API.md) as well as take a look at the [Dynamic Forms Tutorial](/Documentation/Manage/Working with Dynamic Forms.md) before starting.  

 Since there's no need to over-complicate the full capabilities of Dynamic Forms and Charts in this tutorial, we'll not use any Cloud Code in order to create our Dashboard. For this reason we'll only need to create our Chart templates and Analytics Screen.

 In this tutorial we'll create 3 charts:  

* *New Players* \- displays the chart for new player registrations.  
* *Total Players* \- displays the chart for total unique player connections.  
* *Errors & Errors Table* \- a selection of errors we want to track.  

<q>**Note:** The Charts are game-dependent and will be unique for every game. For this reason, some of the charts in this tutorial might use requests that do not exist in your configuration. For example, you might not be able to group requests by: *@type - equal - DeviceAuthenticationRequest* if your game has never made this request. Simply skip these if they are not applicable to you.</q>

### New Players Chart

This chart was created in the *Charts* tab of the *Manage>Admin Screens* section and we used *new_players* Short Code:
* The chart represents the new players entering the game. This is done by grabbing a successful [RegistrationRequest](/API Documentation/Request API/Authentication/RegistrationRequest.md) as well as a successful [DeviceAuthenticationRequest](/API Documentation/Request API/Authentication/DeviceAuthenticationRequest.md) that has been done by a new player (Device Authentication, as well as External Authentications act as a registration for new players):

![](img/CustomAnalyticsDashboards/6.png)

* On the *Test Query* panel, we can define how the chart will display:
  * *Output* - Display the chart as a histogram.
  * *Group By* - Select for no grouping.
  * *Calculation* - Counting only unique players.
  * *Annotate* - Show a tool tip.
  * *Chart Period* - Set the period to *Day*.

We then click *Test* to preview the chart:

![](img/CustomAnalyticsDashboards/7.png)

The chart preview is generated as well as the GSML code, which you can copy and paste into a Screen using the chart later on.

### Total Players Chart

Much like New Players, but here we want to keep track of daily total player logins for the game. For this we need to create a chart with a Short Code of *total_players*:
* Configure the chart to get all different types of authentication - bear in mind that you'll most likely have different Authentications, again, this is per-game basis.

![](img/CustomAnalyticsDashboards/8.png)

* On the *Test Query* panel, we can define how the chart will display:
  * *Output* - Display the chart as a histogram.
  * *Group By* - Select for no grouping.
  * *Calculation* - Counting only unique players.
  * *Annotate* - Show a tool tip.
  * *Chart Period* - Set the period to *Day*.

We then click *Test* to preview the chart:

![](img/CustomAnalyticsDashboards/9.png)

The chart preview is generated as well as the GSML code, which you can copy and paste into a Screen using the chart later on.

### Errors Chart

This chart will be used to display a pie chart and a data table of the error responses for some of the Requests we care about. All we do here is create a chart with *errors* shortCode:
* Find the Responses we're interested in and filter them by the *response.error* value:

![](img/CustomAnalyticsDashboards/10.png)

* On the *Test Query* panel, we can define how the chart will display as a Pie Chart:
  * *Output* - Display the chart as a Pie Chart.
  * *Group By* - Select for grouping by type.
  * *Calculation* - Count of Requests.
  * *Annotate* - Show a legend.
  * *Chart Period* - Set the period to *Day*.

We then click *Test* to preview the chart, which will display the visual representation of the error count that has occurred:

![](img/CustomAnalyticsDashboards/11.png)

* Alternatively, on the *Test Query* panel, we can select to display a Data Table:
  * *Output* - Display the chart as a Data Table.
  * *Page Size* - Select for 5 results per page.

Note that the other display settings for this type of chart are diabled.

We then click *Test* to preview the chart, which will display display and allow viewing of the actual error responses:

![](img/CustomAnalyticsDashboards/12.png)

<q>**Note:** The only difference between these two charts is in how the chart will be accessed by our GSML.</q>

### Analytics Screen

The Screen will only act as a container for our charts. It's fairly straightforward:
* We'll place all of the charts in a Analytics title block.
* Additionally, each chart will have it's own title block explaining what the chart does.
* Since we have 4 chart views, we'll use 2 rows with 2 columns in each row to place the chart in.  

The GSML in the *Analytics* Screen:

```
    <gs-title-block title="Analytics" padding="10" margin="0">

        <gs-row>
            <gs-col width="6">
                <gs-title-block title="New Players" padding="5" margin="0" height="360">
                    <gs-chart chartType='hist' calc='requestCount' annotate='tooltip' chartPeriod='1d' query='new_players'></gs-chart>
                </gs-title-block>
            </gs-col>
            <gs-col width="6">
                <gs-title-block title="Total Players" padding="5" margin="0" height="360">
                    <gs-chart chartType='hist' calc='playerCount' annotate='tooltip' chartPeriod='1d' query='total_players'></gs-chart>
                </gs-title-block>
        </gs-row>
        <br/>

        <gs-row>
            <gs-col width="6">
                <gs-title-block title="Errors" padding="5" margin="0" height="360">
                    <gs-chart chartType='pie' group='_type' calc='requestCount' annotate='legend' query='errors'></gs-chart>
                </gs-title-block>
            </gs-col>
            <gs-col width="6">
                <gs-title-block title="Errors Table" padding="5" margin="0" height="360">
                    <gs-chart chartType='data' pageSize='5' query='errors'></gs-chart>
                </gs-title-block>
            </gs-col>
        </gs-row>
        <br/>

    </gs-title-block>
```

The final view:

![](img/CustomAnalyticsDashboards/5.jpg)

<q>**Note:** All data shown within these forms is time-limited.  Player request data isn't kept forever and it's very likely that when a player has had inactivity for a certain amount of time, the above form can appear empty.</q>
