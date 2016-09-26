---
nav_sort: 6
src: /Tutorials/Cloud Code and the Test Harness/Storing Custom Player Data.md

---

# How to Store Custom Player Data

Typically, you'll want to be able to store custom data against your players so you can consume the data from either Cloud Code or from your game client.

There are two ways you can store custom data against your players:
* Attach data to the player object in Cloud Code.
* Use MongoDB collections to store custom data.

This section describes these two data-storage options and explains the pros and cons of each method.

<q>**More Information!** For further details on how to use the two data-storage mechanisms described here, see the [Managing Data Persistence](/Tutorials/Database Access and Cloud Storage/Managing Data Persistence.md) tutorial.</q>

## Attaching Data to the Player Object in Cloud Code

Attaching player data to the Player object in Cloud Code ensures requests for data will be as fast as possible because the Player object is stored in memory on the GameSparks platform and the Player object is always cached in memory while the player has an open socket.

This data set is best used for data that is shared or stored for the lifetime of the player. You have the ability through the [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md) object to set (this can either add or overwrite), get, and remove data stored against a key.

The SparkPlayer object has 2 separate data sets that differ in their accessibility.

### ScriptData

*ScriptData* can be used to store information against a player that you want to show on a device. The values are stored against the player, and are available via API calls that return details about a player and which means that the data can be accessed:
* The player's device (via [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md)).
* Any of the devices used by the player's friends (via [ListGameFriendsRequest](/API Documentation/Request API/Player/ListGameFriendsRequest.md)).

<q>**Limit ScriptData!** You should limit the amount of data you put into ScriptData. The platform does not limit how much data you can put in but as the data set grows so do the responses that use this data, potentially slowing down request/response times.</q>

### PrivateData

*PrivateData* values are only ever available through Cloud Code, they will never be transmitted to a device.

## Using MongoDB to Store Custom Data

For more complex scenarios, or where you want responses to only include a subset of the data you have stored, we recommend that you create a MongoDB collection to store this data. You can store all options in a single document and use the partial update operations described [here](/Tutorials/Database Access and Cloud Storage/Submitting JSON Document Queries.md).
