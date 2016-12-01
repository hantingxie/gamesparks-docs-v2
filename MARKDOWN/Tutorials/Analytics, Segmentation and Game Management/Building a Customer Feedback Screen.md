---
nav_sort: 6
src: /Tutorials/Analytics, Segmentation and Game Management/Building a Customer Feedback Screen.md
---

# Building a Customer Feedback Screen

This tutorial explains how to set up a basic customer feedback interface that will enable your team to see feedback from your players.

You'll create:
* A feedback collection where entries will be saved.
* An Event which users will use to post their feedback.
* A screen to help you search and view feedback entries.

## Creating a Runtime Collection

Create a runtime collection - for this tutorial we're calling ours *feedback*.

<q>**More Information?** For more details on creating runtime collections see [NoSQL Explorer](/Documentation/NoSQL Explorer.md).</q>

## Creating the Event

The Event is going to have 3 Attributes:

1. The feedback message (String).
2. The level that feedback was submitted for (String).
3. Star rating (Number).

The Event's Cloud Code will take that data and insert the data into the feedback collection as follows:

```
//Load the feedback collection
var feedbackCollection = Spark.runtimeCollection("feedback");

//Insert the new submission
feedbackCollection.insert({"message":Spark.getData().message,
"level":Spark.getData().level,
"stars":Spark.getData().stars,
"player": Spark.getPlayer().getDisplayName()});
```

## The Screens 1 - Snippets

Now we need to design the parts of the screen that will display the feedback to us. So far we have the collection that will save the submissions and the Event which allows our users to submit their feedback.

In this section, we'll set up four snippets for our feedback screen.

<q>**More Information?** For more details on how to work with screens and snippets see [Dynamic Forms](/Documentation/Manage/Working with Dynamic Forms.md).</q>

### Building the Feedback Query

We need to create a search query which will help us display the feedback we want. This will allow us to view feedback that is relevant to certain levels, star score, or the players that posted it.

Handlebars:

```
<gs-query name="feedbackQuery">

     <gs-query-field id="level"
                    label="Level"
                    type='string'
                    operators="equal,begins_with,not_equal"/>

     <gs-query-field id="player"
                    label="Player"
                    type='string'
                    operators="equal,begins_with,not_equal"/>


    <gs-query-field id="stars"
                    label="Stars"
                    type="integer"
                    operators="between,less,less_or_equal,greater,greater_or_equal,exists,not_exists"/>

    </gs-query>
```

### Displaying the Feedback Results

The results screen will display the feedback we wish to display. The message, level, star rating, and player will be available to see. The results screen will also have a button which expands the message into a pop-up screen.

Javascript:

```
Spark.setScriptData("results", SnippetProcessor(Spark.getData().scriptData))

function SnippetProcessor(data){

    var form = {}

    return view(data);

    function view(data){

        query = data.feedbackQuery;

        var feedbackCollection = Spark.runtimeCollection("feedback");
        var numOfResults = feedbackCollection.count();

        form.feedback = feedbackCollection.find(query, {"_id": 1, "message" : 1, "stars" : 1, "player":1,"level":1}).limit(100);
        form.count = form.feedback.count();
        form.overallCount = numOfResults;

        return form;
    }
}

```

Handlebars:

```
<gs-title-block title="Results : {{results.count}} of {{results.overallCount}} cards">
{{#if results.feedback}}
    <gs-row>
        <b>
        <gs-row>
            <gs-col width="5">Message</gs-col>
            <gs-col width="2">Level</gs-col>
            <gs-col width="2">Stars</gs-col>
            <gs-col width="2">Player</gs-col>
        </gs-row>
        </b>
        {{#each results.feedback}}
            <hr/>
            <gs-row>
                <gs-col width="5">{{message}}</gs-col>
                <gs-col width="2">{{level}}</gs-col>
                <gs-col width="2">{{stars}}</gs-col>
                <gs-col width="2">{{player}}</gs-col>
                 <gs-col width="1"><gs-link snippet="feedbackMessage?message={{message}}" target="modal-small"><i class="icon-comment"/></gs-link></gs-col>
            </gs-row>
        {{/each}}
    </gs-row>
{{/if}}
</gs-title-block>
```

### Creating a Feedback Search

This will combine our query and results snippets together in one screen.

Handlebars:

```
<gs-form snippet="feedbackResults" target="feedbackResults">
    <gs-snippet snippet="feedbackQuery"></gs-snippet>
        <gs-col width="12">
            <gs-submit>Submit</gs-submit>
        </gs-col>

</gs-form>

```

### Displaying the Feedback Message

Our final snippet will be a pop-up that displays the feedback on its own.

Javascript:

```
Spark.setScriptData("form", SnippetProcessor(Spark.getData().scriptData))

function SnippetProcessor(data){

    var form = {};

    return view(data);

    function view(data){

        form.message = data.message;
        return form;
    }
}

```

Handlebars:

```
<gs-title-block title="Feedback" margin="0" padding="10">
    <gs-row >
                {{form.message}}
            </gs-row>
</gs-title-block>

```
</br>
So to recap, we have 4 snippets.

1. Query snippet.
2. Results snippet.
3. Search snippet, which is a combination of 1 and 2.
4. Message snippet.

## The Screens 2 - Screen

The screen will house our snippets to allow us to view the feedback. Create a screen and add the following code:

```

<gs-row>
    <gs-title-block title="Feedback" padding="10">
        <gs-row>
            <gs-snippet snippet="feedbackSearch"></gs-snippet>
        </gs-row>
    </gs-title-block>
</gs-row>

<gs-row>
    <gs-placeholder id="feedbackResults"></gs-placeholder>
</gs-row>

```
</br>
Your feedback feature is now ready to use:
* Authenticate and use the feedback event to post a mock feedback.
* Check your collection using NoSQL to see if the submission was successful.
* If the submission is successful, check your screen in the manage section to see if the dynamic forms were created successfully.
