---
nav_sort: 6
src: /Tutorials/Database Access and Cloud Storage/Managing Data Persistence.md
---

# Managing Data Persistence in the GameSparks Platform

Customers frequently ask how to persist various types of data on the GameSparks platform. This tutorial provides a guide to best-practices for managing data persistence on the platform.

Here's an overview of our recommendations:

* **Player Data.** Small amounts of player-related data can be stored on the Player collection in either *scriptData* or *privateData*.
* **Custom Collections.** Larger structured data should be stored in either metadata or runtime collections.
* **Binary Assets.** Binary assets and data should be stored using Downloadables and Uploadables.
* **Transient Data.** Transient data that requires fast operations can be stored in Redis.

By spending some time choosing the correct storage for your data to serve your specific requirements, you can improve the performance of your game and avoid scalability issues further down the line. Ultimately, this will lead to happier players who are more likely to return to your game again and again!



## Player Data

The system Player collection offers two ways to store custom data (in addition to the standard data stored for a player such as currency, virtual goods, and so on). These are designed for storing key-value pairs, although note that the “value” can be a either a simple value, or a complex JSON object, allowing structured data to be stored if required.

### scriptData

The first method for storing data in this way is to use *scriptData*. This can be set and retrieved using Cloud Code as follows:

```

Spark.getPlayer().setScriptData("myCustomData", { "subKey" : 1 } );

var myCustomData = Spark.getPlayer().getScriptData(“myCustomData”);


```

Any data stored in *scriptData* is available via the GameSparks API for authenticated players. That is, it will be returned to client devices in responses to requests including *AccountDetailsRequest* and *ListGameFriendsRequest*.

For example, sending an *AccountDetailsRequest*:

```

{  "@class": ".AccountDetailsRequest" }

Would return a response similar to:

{
 "@class": ".AccountDetailsResponse",
 "currency1": 0,
 "currency2": 0,
 "currency3": 0,
 "currency4": 0,
 "currency5": 0,
 "currency6": 0,
 "displayName": "Test Player",
 "externalIds": {},
 "reservedCurrency1": {},
 "reservedCurrency2": {},
 "reservedCurrency3": {},
 "reservedCurrency4": {},
 "reservedCurrency5": {},
 "reservedCurrency6": {},
 "scriptData": {
  "myCustomData": {
   "subKey": 1
  }
 },
 "userId": "5784b7a9e62308e1ec7a51c8",
 "virtualGoods": {}
}

```
</br>
### privateData

*privateData* is similar to *scriptData* except this data is never sent to clients via normal API requests. This is always retrieved via Cloud Code only:

```

Spark.getPlayer().setPrivateData("myPrivateData", { "secretStuff" : 1 } );

var myPrivateData = Spark.getPlayer().getPrivateData(“myPrivateData”);

```

So, even if the player has some *privateData* set, only the *scriptData* will be returned using API calls – the result of an *AccountDetailsRequest*, for example, would be exactly the same as the example above even after setting *privateData*.

### Using scriptData and privateData

These two mechanisms are perfect for when you have a small amount of data that is associated with a player:
* The data will be stored for the lifetime of the player (although it may be updated using Cloud Code).
* The data is structured JSON, so can be used in a meaningful way in code.
* *scriptData* provides an easy mechanism to share this information about a player between clients, such as a public profile containing avatar information, or, for example, hair color, eye color, and so on.

However, storing large amounts of data this way is not recommended. Every time a player is accessed - one of the most common things to do on the platform - this data is retrieved and, in the case of *scriptData*, sent to clients in responses. This reduces performance and increases your bandwidth usage, leading to reduced responsiveness on the client. For this reason use these methods to store data only for data that is:
* Small in size.
* Really needs to be returned to the client every time you request the player data should be stored this way.

</br>
So what if you need to store larger volumes of data that is only accessed on-demand? In this case, you probably want to explore *Custom Collections*.

## Custom Collections

Custom collections allow you to store large, complex, structured data in MongoDB which can be accessed on-demand through Cloud Code.

There are two types of custom collections:
* **Metadata collections** are read-only at runtime. These are perfect for storing metadata (hence the name) in your game, such as static-level configuration, descriptions of characters in the game, and so on.
* **Runtime collections**, by contrast, can be altered at runtime, and should be used for storing data generated at runtime and not static configuration data.

Collections can be created on-the-fly in MongoDB. The first time you access a runtime collection, if it doesn’t exist, it will be created. For example:

```

var query = { "_id":"12345" };
var data = Spark.runtimeCollection("largeData").find(query);

```

This method will work, even if the “largeData” collection has never been explicitly created. However, it will return a cursor with no documents in it.

Storing data in a runtime collection is also achieved in Cloud Code:

```

var doc = { "gameState": { "gameType": "deathMatch" } };
Spark.runtimeCollection("largeData").save(doc);


```

Storing data in custom collections means that the data can be queried and (in the case of runtime collections) modified easily at run-time. It also provides all the power and flexibility that MongoDB has to offer.


### Indexing Custom Collections

Custom collections can (and often should) be indexed for performance reasons. For example, if you always access the data by a field called “gameType” then you should index the collection as follows:

```

Spark.runtimeCollection("largeData").ensureIndex({"gameState.gameType":1});


```

This will create an ascending index on the “gameType” field. You should place the calls to *ensureIndex* for your collections in the Game Published system script, to ensure they are only called once for each collection (or more specifically, once per collection per game version that is published). There would be a slight overhead placing *ensureIndex* calls in a regularly executed Event script, for example.



### Common Mistakes with Runtime Collections

There are two common mistakes to avoid when storing data in runtime collections:
* The first common mistake is in how the data is populated in the first place. It's generally a bad idea to pass up the entire document from the client and persist it to the database. It's much better to either pass up data from clients representing the change in state for the data, rather than the entire data itself. Persisting the entire document every time (rather than just altering the document to store the new data) can lead to performance problems for your game for two reasons:
  * First, you are passing a lot of data over the network, which takes time and reduces the responsiveness of your game for your customers.
  * Second, saving the entire document every time also means a lot of data being passed to MongoDB unnecessarily, which places unnecessary load on the underlying database. So in effect this is a double-whammy. Although it may work for a small number of players, as your player-base increases this kind of design becomes a problem. Try to pass up only the changes that have been made, and persist those into the document instead.

* The second common mistake is to attempt to store binary data in a collection.
  * For example, you may think that encoding some binary data using Base64 and saving it to MongoDB is a sensible idea. On the face of it, this sounds like a good idea. However, it breaks the guidelines given above – the data is not formatted in a way that it can be queried and manipulated easily in Cloud Code (that is, it's not JSON format). The almost certain result is that you would have to pass the entire data from client to server every time.

</br>
If you do need to store binary data in GameSparks, such as uploading a file, you should probably be using *Binary Assets*.


## Binary Assets

Binary assets fall into two categories: *Uploadables* and *Downloadables*.

### Uploadables

Uploadables are files that, as the name suggests, are uploaded from a client device:
* Perfect for storing binary data created by players at runtime.
* Can later be downloaded to other devices to share file-type data between devices.

To upload data, a client device would first make an API call to GameSparks to retrieve an upload URL:

```

{ "@class": ".GetUploadUrlRequest" }


```

This will return a URL in the response:

```
{
 "@class": ".GetUploadUrlResponse",
 "url": "https://gsp-aeu001-se04.gamesparks.net/upload/351233XEAriw/56e91d8377588b04932481d8/51aada5dc51c4c7daf08a4b9a4136be5?gsstage=live"
}

```

The client device can then upload the binary data to the given URL, and receives an *UploadCompleteMessage*, which contains amongst other things, an *uploadId*:

```

{
 "@class": ".UploadCompleteMessage",
 "messageId": "5784cee777588b670617c090",
 "notification": true,
 "playerId": "56e91d8377588b04932481d8",
 "summary": "Your upload is complete",
 "uploadData": {
  "fileName": "51aada5dc51c4c7daf08a4b9a4136be5-portal.jpeg",
  "uploadId": "51aada5dc51c4c7daf08a4b9a4136be5",
  "fileSize": 9639,
  "origFileName": "portal.jpeg",
  "playerId": "56e91d8377588b04932481d8",
  "fileId": "ABC.12345"
 },
 "uploadId": "51aada5dc51c4c7daf08a4b9a4136be5"
}

```

You would then typically store this *uploadId* along with whatever other data you needed (for example, playerId, information about the level they were on, or any other relevant metadata) into your own custom runtime collection so you can retrieve it later.

Once uploaded, data can be retrieved (by either the same client or any other client connected to the game) by querying the custom runtime collection to find the *uploadId*, then sending a *GetUploadedRequest*:


```

{
 "@class": ".GetUploadedRequest",
 "uploadId": "51aada5dc51c4c7daf08a4b9a4136be5"
}

```

The response to this request contains a URL, which the client can then use to download the data:

```

{
 "@class": ".GetUploadedResponse",
 "size": 9639,
 "url": "https://gamesparksbinaries.blob.core.windows.net/upload-351233/51aada5dc51c4c7daf08a4b9a4136be5-portal.jpeg?sig=r4MGQ%2F9ulSftiHvDd08JWseo23s%2Bh8jftDWEaLxehVo%3D&st=2016-07-12T11%3A02%3A47Z&se=2016-07-12T11%3A17%3A47Z&sv=2015-04-05&sp=r&sr=b&gsstage=live"
}

```

### Downloadables

Downloadables, on the other hand, are only available for downloading to client devices. These:
* Should be used to store static binary assets for your game, which are common between players.
* Can be created from within the Web Portal in the Configurator, and downloaded by players in a similar way to Uploadables via a *GetDownloadableRequest* (passing in the short code configured in the Web Portal for the downloadable asset):

```

{
 "@class": ".GetDownloadableRequest",
 "shortCode": "DL1"
}

```

which returns the URL to download the asset from:

```

{
 "@class": ".GetDownloadableResponse",
 "lastModified": "2016-03-10T16:16Z",
 "shortCode": "DL1",
 "size": 300109,
 "url": "https://gamesparksbinaries.blob.core.windows.net/game-351233/1457626590618/axn-sean-bean-reddit-ama-6.jpg?sig=8gUTRizdXoWwKXVL5E28jG0uOXH5l7Dju%2FHT9HULsAg%3D&st=2016-07-12T11%3A06%3A04Z&se=2016-07-12T11%3A21%3A04Z&sv=2015-04-05&sp=r&sr=b&gsstage=live"
}

```
</br>
There is one final data store available to the GameSparks platform: *Redis Data*.

## Redis Data

If you want a fast way to store simple data structures as key-value pairs, you also have access to a Redis instance for your game. Redis is:
* A fast, efficient, in-memory data store and is significantly faster than MongoDB for storing and retrieving small quantities of data.
* The option of choice when you want to perform fast data manipulation on transient data, such as Set operations, numeric sorting of data, and so on.

Access to the Redis datastore is achieved, as usual, through Cloud Code. To store a simple set of values:

```

Spark.getRedis().sadd("MySet", 1);
Spark.getRedis().sadd("MySet", 2);
Spark.getRedis().sadd("MySet", 1);

```

This would result in two values (the numbers 1 and 2) being stored in a set against the key of “MySet”.

Redis is very powerful but can have a bit of a learning curve in comparison to other data stores. For a guide on what Redis is capable of and how to use it, the best source is probably the official Redis website at [redis.io](https://redis.io/).
