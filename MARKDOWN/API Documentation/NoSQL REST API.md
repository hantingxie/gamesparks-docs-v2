---
nav_sort: 2
src: /API Documentation/NoSQL REST API.md
---

# NoSQL Explorer REST API

<q>**Read First!** This NoSQL Explorer REST API page assumes you've already read the [REST APIs Overview](/API Documentation/REST APIs/README.md) page.</q>

The GameSparks platform allows you to manage the data you store in the MongoDB and Redis databases via a REST interface. You can use this REST API to control your game's data stored in these databases directly and without having to do this via the GamesSparks platform.

All the communication is based on a JSON payload.

## Authentication

See the [REST API Overview](/API Documentation/REST APIs/README.md) page where authentication is explained.

## Discovering the Endpoint

In the system architecture diagram on the [REST API Overview](/API Documentation/REST APIs/README.md) page you can see that there are multiple servers that handle the NoSQL REST requests, one for each cluster. This means that before you can query the system for NoSQL information, you must first find out what server you need to talk to.

**Request**
```
GET https://config-beta.gamesparks.net/restv2/game/{gameApiKey}/endpoints
```

**Example response**
```
{
  "liveNosql": "https://gsp-aeu004-cluster.gamesparks.net",
  "previewNosql": "https://gsp-aeu000-cluster.gamesparks.net",
  "liveElasticSearch": "https://gsp-aeu004-es.gamesparks.net",
  "previewElasticSearch": "https://gsp-aeu000-es.gamesparks.net"
}

```
You'll use either the *previewNosql* or the *liveNosql* base URLs, depending on the stage you want to query: Preview or Live respectively.

From now on, we'll refer to the endpoint you choose to query as {stageBaseUrl}.

## Examples
You can find an exhaustive list of the operations that you can perform using the NoSQL Explorer REST API together with an explanation of their parameters [here](/API Documentation/REST APIs/NoSQL.md).

This section provides a few examples.

### Find all collections
```
GET {stageBaseUrl}/restv2/game/{gameApiKey}/mongo/collections
```
Returns all the available collections and the operations you are allowed to perform on each of them.

#### Example response
```
[
  {
    "actions": [ "FIND", "COUNT", "INSERT", "UPDATE", "REMOVE", "INDEX", "AGGREGATE", "STATS"],
    "name": "challengeInstance",
    "optionGroup": "System"
  },
  {
    "actions": [ "FIND", "COUNT", "INSERT", "UPDATE", "REMOVE", "INDEX", "AGGREGATE", "STATS"],
    "name": "externalAuthentication",
    "optionGroup": "System"
  },
  {
    "actions": [ "FIND", "COUNT", "INSERT", "UPDATE", "REMOVE", "INDEX", "AGGREGATE", "STATS" ],
    "name": "player",
    "optionGroup": "System"
  },
  {
    "actions": [ "FIND", "COUNT", "INDEX", "AGGREGATE", "STATS" ],
    "name": "score-leaderboard",
    "optionGroup": "Leaderboards"
  },
  {
    "actions": [ "FIND", "COUNT", "INSERT", "UPDATE", "REMOVE", "INDEX", "AGGREGATE", "DROP", "STATS"],
    "name": "score-runningTotal",
    "optionGroup": "Running Totals"
  }
]
```

### Find data in a collection

```
POST: {stageBaseUrl}/restv2/game/{gameApiKey}/mongo/collection/player/find
```

This example will return the players that match the parameters you passed

  * *query* : The query you want to execute in JSON form:
    * To find players with displayName "testUser" the following JSON should be used {"displayName" : "testUser"}.
  * *sort* : The JSON representation of the sort for the query:
    * To sort by userName in ascending order the following JSON should be used {"userName" : 1}.
  * *fields* : Allows you to limit the fields that are returned in the results. This is useful for collections with large documents:
    * To limit the results to only contain the userName and currency1 the following JSON should be used : {"userName" : 1, "currency1" : 1}. 1 indicates inclusion and 0 indicates exclusion for a field. You cannot mix inclusion and exclusion in a single query.
  * *skip* : The number of documents to skip, useful for paging in combination with limit.
  * *limit* : The maximum number of documents to return. The maximum that the limit value can be set to is 10000.


#### Example Request
```
{
	"query":{"displayName":"testUser"},
	"fields":{"userName":1,"currency1":1},
	"skip":0,
	"sort":{"userName":1},
	"limit":100
}
```

#### Example Response

```
[
  {
    "_id": {
      "$oid": "58b826d0b5973404c700a925"
    },
    "userName": "gamedude",
    "currency1": {
      "$numberLong": "1"
    }
  }
]
```
### Create a meta collection

You can only create meta collections or runtime collections. The following request will create a meta collection called 'tracks':
```
POST {stageBaseUrl}/restv2/game/{gameApiKey}/mongo/collection/tracks/meta
```
**Response**
```
{message: "OK"}
```
