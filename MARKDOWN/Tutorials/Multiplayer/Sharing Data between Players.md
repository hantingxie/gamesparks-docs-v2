---
nav_sort: 3
src: /Tutorials/Multiplayer/Sharing Data between Players.md
---

# Sharing Data between Players

The GameSparks platform makes it easy for developers to be able to share game data between players. You may want to use this to implement features such as:
* Ghost data replay in a racing game.
* Sharing player-created game levels.

In this article, we'll work through an example of how to share ghost race data that would allow a game to display another player's previous attempt at a track/level within a simple racing game. To do this, we'll create Event and Cloud Code scripts within the GameSparks Developer Portal and then test the configuration using the Test Harness.

## Key Concepts

We will need to create an Event which we can use to post the ghost data into GameSparks when a player completes a race on a given track. This Event will have a Cloud Code script attached to it that stores the ghost data in the Mongo database. A second Event and Cloud Code script will be used to allow the game to query the ghost data collection for a given track and retrieve the player's ghost that represents the fastest time on this track.

For the purpose of this article we will assume that the ghost race data can be represented by the following JSON document:
* The *tick* field is the game's animation counter.
* The *xPosition* and *yPosition* are the coordinates of the player in the game world.
* The *heading* field represents the direction that the player is facing within the game world.

```    
[
  {
    "tick":number,
    "xPosition":number,
    "yPosition":number,
    "heading":number
  }
]
```  

## Creating the Event and Cloud Code Script for Storing Ghost Data

*1.* Create an Event that allows the game to submit the JSON ghost race data, the track name and the race time (how long the race took):
* Log in to the GameSparks Portal and navigate to *Configurator > Events*.
* Click to *Add* a new Event.
* Set up the Event as follows:

![](img/PlayerDataSharing/5.png)

*2.* Click to *Save and Close* the new Event.

*3.* Create the Cloud Code script to store this data in a MongoDB collection:
* In the Portal navigate to *Configurator > Cloud Code > Scripts > Events*.
* Select the *STORE_RACE_DATA* Event we created in the previous section:

![](img/PlayerDataSharing/6.png)

* Copy and paste in the following Cloud Code script in to the Cloud Code editor and click *Save*.

```    
  // Get the incoming Event Attributes
  var ghostData = Spark.getData().GHOST_DATA;
  var trackName = Spark.getData().TRACK;
  var timeTaken = Spark.getData().TIME;

  // Create a Mongo collection in which to store the data
  var raceData = Spark.runtimeCollection('raceData');

  // Store the Event data along with the playerId
  var playerId = Spark.getPlayer().getPlayerId();
  raceData.save({"ghostData":ghostData, "trackName":trackName, "timeTaken":timeTaken, "playerId":playerId});

```    

### Testing the Configuration

We will now use the Portal Test Harness and NoSQL Explorer to test the configuration and check the results.

*1.* Navigate to the Test Harness and under *Requests* click *Authentication*. Select *RegistrationRequest* and submit a request to register a new player, PlayerNI:

```    
  {
   "@class": ".RegistrationRequest",
   "displayName": "Player One",
   "password": "password",
   "userName": "playerN1"
  }
```

*2.* Now click *LogEvent* under *Requests* and select the *Store race data* Event we created earlier and send the following *LogEventRequest*.

* Note that for simplicity in this example we are only sending an array of ghost data containing three items in this article but in reality this array would be much larger.

```    
  {
   "@class": ".LogEventRequest",
   "eventKey": "STORE_RACE_DATA",
   "GHOST_DATA": [
   {
   "tick": 1,
   "xPosition": 0,
   "yPosition": 0,
   "heading": 90
   },
   {
   "tick": 2,
   "xPosition": 10,
   "yPosition": 0,
   "heading": 92
   },
   {
   "tick": 3,
   "xPosition": 20,
   "yPosition": 0,
   "heading": 94
   }
   ],
   "TRACK": "Track1",
   "TIME": 90
  }

```

If successful you'll get a *LogEventResponse* similar to this.

```    
  {
   "@class": ".LogEventResponse",
  }
```

*3.* Now, navigate to the *NoSQL Explorer* and under *Collections* expand *Runtime* and select *script.raceData*.

*4.* Click *Find*:
* You'll see the document that was saved as a result of our Cloud Code script executing when the Event was received - this is returned into the *Output* panel.
* You can click on the document to expand, edit, or delete it.

![](img/PlayerDataSharing/7.png)

*5.* Repeat the sending of the *Store race data* Event but change the data each time, especially the *TIME* field. This will result in several documents being stored in MongoDB for PlayerN1.

*6.* Now register a second player, PlayerN2, by sending a *RegistrationRequest* and repeat the sending of the *Store race data* Event. Change the data each time, especially the *TIME* field. This will result in several documents being stored in MongoDB for PlayerN2.

## Creating the Event and Cloud Code Script for Retrieving Ghost Data

Now we need to create an Event that allows the game to retrieve the fastest player's JSON ghost race data for a given track name.

### Creating the Data Retrieval Event

*1.* Navigate to *Configurator > Events*.

*2.* Click to *Add* and a new Event.

*3.* Set up the Event as follows:

![](img/PlayerDataSharing/8.png)

*4.* Click to *Save and Close* the new Event.

### Adding Cloud Code to the Data Retrieval Event

Next we create the Cloud Code script to retrieve the data from the MongoDB collection and return it in the *LogEventResponse*.

*1.* Navigate to *Configurator > Cloud Code > Scripts > Events*.

*2.* Select the *GET_RACE_DATA* Event we created in the previous section.

*3.* Copy and paste the following Cloud Code into it:

```    
  // Get the incoming Event Attribute
  var trackName = Spark.getData().TRACK;

  // Find the fastest race data for the given track
  var fastestRaceData = Spark.runtimeCollection('raceData').find({"trackName":trackName}).sort({"timeTaken":1}).limit(1);

  // Return the race data in the response
  Spark.setScriptData("fastestRaceData", fastestRaceData);

```

*4.* Click to *Save* the Cloud Code script on the Event.

### Testing the Configuration

We'll now use the Test Harness to test the configuration and check the results.

*1.* Navigate to the Test Harness, under *Scripts* click *Authentication*, and select *AuthenticationRequest*.

*2.* Send the *AuthenticationRequest* for PlayerN2 that you registered at step *6.* when [testing](#Testing the Configuration) the storage Event we set up and which should be something like this:

```    
  {
   "@class": ".AuthenticationRequest",
   "userName": "playerN2",
   "password": "passwordN2"
  }
```

*2.* Now, click *Log Event* and select the *Retrieve race data* Event we just created and send a *LogEventRequest* for track 1:

```    
  {
   "@class": ".LogEventRequest",
   "eventKey": "GET_RACE_DATA",
   "TRACK": "Track1"
  }

```

The response will look similar to this and should be the fastest *timeTaken* document from the collection for the given track.

```    
{
  "@class": ".LogEventResponse",
  "scriptData": {
    "fastestRaceData": [
      {
        "_id": {
          "$oid": "583434b73a32df04a72a56d5"
        },
        "ghostData": [
          {
            "tick": 1,
            "xPosition": 0,
            "yPosition": 0,
            "heading": 90
          },
          {
            "tick": 2,
            "xPosition": 10,
            "yPosition": 0,
            "heading": 92
          },
          {
            "tick": 3,
            "xPosition": 20,
            "yPosition": 0,
            "heading": 94
          }
        ],
        "trackName": "Track1",
        "timeTaken": 89,
        "playerId": "5834348e3a32df04a72a539c"
      }
    ]
  }
}
```
