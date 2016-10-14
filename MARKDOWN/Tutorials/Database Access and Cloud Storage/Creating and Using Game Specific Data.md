---
nav_sort: 7
src: /Tutorials/Database Access and Cloud Storage/Creating and Using Game Specific Data.md
---

# How to Create and Use Game Specific Data

You might want to make game-specific data, either static data or global variables, available to every player or to requests made to the server. An example could be a global message of the day, or a notification to tell players they must have the latest version of the app in order to gain access to multiplayer features. There are two ways of creating and using game-specific data, through *Static Declaration* and *Dynamic Declaration*.

## Declaring the Data

### Static Declaration

If you don’t want to dynamically add and modify these values, instead you simply want to declare them, it’s very easy to do - here's how:

*1.* Create an Event with a string attribute. You'll use this string attribute to reference which data you'll be retrieving.

*2.* When the Event is created, go to the Cloud Code section and edit the Event’s Cloud Code. Our Cloud Code for retrieving manually declared data will look like this:

```
//String attribute from event which tells us which data we need
var dataKey = Spark.getData().dataKey;

//Random manually declared data for game data purposes stored in an object
var dataOBJ = { messageOfDay : "Hey there today is the 11th of April!", versionNum : 1.234};

//Return tphe data object with the data we asked for
Spark.setScriptData("data", dataOBJ[dataKey]);

```

*3.* Using a logEvent request from the SDK you can retrieve this data as scriptData from the response.


### Dynamic Declaration

This is straightforward, but requires you to set up a few things - we'll walk you through it step by step:

*1.* Head over to the NoSQL tab on the platform.

*2.* Click the 'Create' tab and create a Runtime collection. For this tutorial we will name it 'gameData'.

*3.* Click the insert tab and create a string value for messageOfDay like this:

```

{messageOfDay:"Hey there today is the 11th of April!"}

```

*4.* After inserting that document we can dynamically add values to it. To do so we need to create an Event to set data with one string attribute for key. This is so we can reference it later and add a JSON attribute value to store (Numbers and Strings can also be input).

*5.* When that Event is created, navigate to the Cloud Code section and edit the code. In this example, we have:

```

//Declare key and data from attributes passed in
var dataKey = Spark.getData().dataKey;
var dataVal = Spark.getData().dataVal;

//Retrieve game data collection
var gameDataCollection = Spark.runtimeCollection("gameData");

//Build data using keyValue pair and data
var dynamicJSON = {dataKey:dataVal};

//Update the collection using the $set function - we're using the _id field to find the document
gameDataCollection.update({_id: {"$oid": "570ba4f37f416a06026e5cc8"}}, {$set:dynamicJSON});

```

*6.* Head over to the [Test Harness](/Documentation/Test Harness/README.md) and authenticate.

*7.* Call the Event with the key 'messageOfDay' and a string or JSON value, like this:

```

{
 "@class": ".LogEventRequest",
 "eventKey": "setData",
 "dataKey": "messageOfDay",
 "dataVal": "It's now the 12th of April!"
}

```

*8*. When the Event has been called, navigate to the NoSQL explorer and click the 'find' tab.

*9.* Select your gameData collection and click the find button to bring up the document which includes the data. You should now see that the value is present.

*10.* To retrieve the data from the collection, create an Event with one string attribute which will refer to the key of the data. The Cloud Code will look like this:

```
//Decare the dataKey variable as the string attribute passed in
var dataKey = Spark.getData().dataKey;
//Retrieve the game data collection
var gameDataCollection = Spark.runtimeCollection("gameData");

//Retrieve the game data object
var dataJSON = gameDataCollection.findOne();

//Retrieve the data from the object using the name passed in (dataKey)
var dataValue = dataJSON[dataKey];

//Return the data through scriptData
Spark.setScriptData("data", dataValue);

```

*11.* Using a logEvent request from the SDK you can retrieve this data as scriptData from the response.

This is how to dynamically set and retrieve game-specific data. You can add further queries, settings, and layers of complexity to your setup. These are the fundamental steps to do so. You can also add extra documents to your game data collection to house different kinds of data and refer to the different documents for specific purposes. GameSparks ensures endless possibilities are open to you and enables you to customize the experience to suit the needs of your projects.
