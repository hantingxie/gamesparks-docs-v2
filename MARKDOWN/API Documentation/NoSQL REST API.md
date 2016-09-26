---
nav_sort: 2
src: /API Documentation/NoSQL REST API.md
---

# NoSQL Explorer REST API

The GameSparks platform allows you to manage your NoSQL data via a REST interface. This is useful to allow you to control your game data via your own software. This REST API provides the same features found in the GameSparks Developer Portal [NoSQL Explorer](/Documentation/NoSQL Explorer.md).

## Authentication

All REST API methods require the use of HTTP Basic Authentication to authenticate with the service;
* You need to provide the username and password you use to login to the portal.
* The REST endpoint is secured over HTTPS, so there's no need to worry about your credentials being exposed.
* To authenticate using Basic Authentication you will need to provide an "Authorization" header. The Authorization header is constructed as follows:
  * Username and password are combined into a string "username:password".
  * The resulting string literal is then encoded using the RFC2045-MIME variant of Base64, except not limited to 76 char/line[9].
  * The authorization method and a space, that is, "Basic " is then put before the encoded string.
  * For example, if the user agent uses 'Aladdin' as the username and 'open sesame' as the password, then the header is formed as follows:
    * Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

## Find Data

Find data using the following URL. *POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/find*

#### Parameters

  * *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
  * *stage* : Indicates which database stage to use - *Preview* or *Live*.
  * *collection* : Indicates which collection to perform the action against.

#### Form Data (optional)

  * *query* : The query you want to execute in JSON form:
    * To find players with displayName “testUser” the following JSON should be used {“displayName” : “testUser”}.
  * *sort* : The JSON representation of the sort for the query:
    * To sort by userName in ascending order the following JSON should be used {“userName” : 1}.
  * *fields* : Allows you to limit the fields that are returned in the results. This is useful for collections with large document:
    * To limit the results to only contain the userName and displayName the following JSON should be used : {“userName” : 1, “displayName” : 1}. 1 indicates inclusion and 0 indicates exclusion for a field. You cannot mix inclusion and exclusion in a single query.
  * *skip* : The number of documents to skip, useful for paging in combination with limit.
  * *limit* : The maximum number of documents to return. The maximum that the limit value can be set to is 10000.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/player/find

#### Example Response

```
    [
     {
     "_id": {
     "$oid": "536ce4aa4566340888d2d969"
     },
     "_class": "com.gamesparks.common.domain.Player",
     "gameId": 161,
     "deviceRegIds": {},
     "goods": {},
     "achievements": [],
     "currency1": 1,
     "reservedCurrency1": {},
     "currency2": 2,
     "reservedCurrency2": {},
     "currency3": 3,
     "reservedCurrency3": {},
     "currency4": 4,
     "reservedCurrency4": {},
     "currency5": 5,
     "reservedCurrency5": {},
     "currency6": 6,
     "reservedCurrency6": {},
     "authTokens": [
     "fda60fce-0ee8-4efb-beb6-ffd99b459bbe",
     "aa40b641-987f-4ee3-b2e9-a114e5bf1ce5",
     "6876d991-8714-4a1c-8266-e871ab0face9"
     ],
     "userName": "gamedude",
     "displayName": "G-D",
     "password": "*******",
     "online": true,
     "scriptData": {},
     "privateData": {},
     "externalAuthentications": {},
     "externalIds": {},
     "created": 1399645354792
     }
    ]
```

## Insert Data

Insert data using the following URL. *POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/insert*

#### Parameters

  * *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
  * *stage* : Indicates which database stage to use - *Preview* or *Live*.
  * *collection* : Indicates which collection to perform the action against.

#### Form Data

  * *document* : The JSON document to insert into the collection.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/insert

Form Data - document : {"my key" : "my value"}

#### Example Response

```
    [
     {
     "my key" : "my value",
     "_id": {
     "$oid": "53981dc11566f815c375419d"
     }
     }
    ]
```

## Update Data

Update data using the following URL. *POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/update*

#### Parameters

  * *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
  * *stage* : Indicates which database stage to use - *Preview* or *Live*.
  * *collection* : Indicates which collection to perform the action against

#### Form Data

  * *query* (optional) : The selection criteria for the update. Use the same query selectors as used in the Find method.
  * *update* : The modifications to apply. 
  * *multi* (optional) : Set to true if all documents meeting the criteria should be modified. Defaults to false.
  * *upsert* (optional) : Set to true to create a new document when no document matches the query. Defaults to false.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/update

Form Data - query : { "\_id": "my key" }, update : {"my data":"new value"}

#### Example Response

```
    [
     {
     "_id": "my key",
     "my data":"new value"
     }
    ]
```

## Remove Data

Remove data using the following URL. *POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/remove*

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against

#### Form Data

  * *query* : The selection criteria for the Remove operate. All documents matching this criteria will be removed.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/remove

Form data - query : {"\_id": { "$oid": "539707414566be9a5c0ff373"}}

#### Example Response

```
    {
     "message": "Affected Rows : 1"
    }
```

## Aggregate Data

Aggregate data using the following URL. *POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/aggregate*

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against

#### Form Data

  * *pipeline* : A JSON array of pipeline commands. If you are supplying more than one pipeline stage you must wrap then within a JSON array.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/aggregate

Form data - pipeline : [{ "$match" : { "startTime" : { "$gte" : { "$date" : "2014-05-31T23:00:00.000Z"} , "$lte" : { "$date" : "2014-06-11T09:19:01.549Z"}}}},{ "$project" : { "time-group" : { "$substr" : [ "$startTime" , 0 , 7

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/aggregate

 Form data - pipeline : [{ "$match" : { "startTime" : { "$gte" : { "$date" : "2014-05-31T23:00:00.000Z"} , "$lte" : { "$date" : "2014-06-11T09:19:01.549Z"}}}},{ "$project" : { "time-group" : { "$substr" : [ "$startTime" , 0 , 7]} , "sum" : "$sum" , "count" : "$count"}},{ "$group" : { "\_id" : "$time-group" , "sum" : { "$sum" : "$sum"} , "count" : { "$sum" : "$count"}}},{ "$project" : { "\_id" : "$\_id" , "AvgSessionTime" : { "$divide" : [ "$sum" , "$count"]}}},{ "$sort" : { "\_id" : 1}}]

#### Example Response

```
{ "_id": "2014-06", "AvgSessionTime": 0 }
```

## Create a Collection

Create a collection using the following URL.

POST: /rest/games/{gameApiKey}/mongo/*{stage}/{collection}*/create 

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against.


#### Form Data

*   *collectionType :* 'script' for a runtime collection (not included in game snapshots) or 'meta' for a meta collection (included in game snapshots).

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/alienbases/create

Form data - collectionType : meta

#### Example Response

```
{
 "message": "Created collection meta.alienbases"
}
```

## Drop a Collection

Drop a collection using the following URL.

*POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/drop*

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against. Note that runtime collections that you create have their names prefixed with 'script.' and meta collections that you create have their names prefixed with 'meta.'.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/weapons/drop

#### Example Response

```
{
 "message": "Dropped collection weapons"
}
```

## Show Collection Statistics

Show collection statistics using the following URL.

POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/stats

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/analysis/stats

#### Example Response

```
{
 "serverUsed": "localhost:27017",
 "ns": "161-game-preview.analysis",
 "count": 578,
 "size": 284720,
 "avgObjSize": 492,
 "storageSize": 696320,
 "numExtents": 4,
 "nindexes": 1,
 "lastExtentSize": 524288,
 "paddingFactor": 1,
 "systemFlags": 1,
 "userFlags": 1,
 "totalIndexSize": 32704,
 "indexSizes": {
 "_id_": 32704
 },
 "ok": 1
}
```

## Show Database Statistics

Show database statistics using the following URL.

POST: /rest/games/{gameApiKey}/mongo/{stage}/dbstats

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/dbstats

#### Example Response
```
{
 "serverUsed": "localhost:27017",
 "db": "161-game-preview",
 "collections": 83,
 "objects": 8493,
 "avgObjSize": 207.146591310491,
 "dataSize": 1759296,
 "storageSize": 6643712,
 "numExtents": 117,
 "indexes": 116,
 "indexSize": 1340864,
 "fileSize": 67108864,
 "nsSizeMB": 16,
 "dataFileVersion": {
 "major": 4,
 "minor": 5
 },
 "extentFreeList": {
 "num": 4,
 "totalSize": 2760704
 },
 "ok": 1
}
```

## Count

Count the number of documents in a collection that match a *Find* query using the following URL.

POST: /rest/games/{gameApiKey}/mongo/{stage}/{collection}/count

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against.

#### Form Data (optional)

*   *query* : The query you want to execute in JSON form:
  * To find players with displayName “testUser” the following JSON should be used {“displayName” : “testUser”}.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/player/count

#### Example Response

```
{
 "count": 3103092
}
```

## Index

View the indexes that have been created for a Collection.

#### Parameters

* *gameApiKey* : The API key of your game, which you can find on the *Overview* page of the Portal Configurator.
* *stage* : Indicates which database stage to use - *Preview* or *Live*.
* *collection* : Indicates which collection to perform the action against.

#### Example Request

POST: https://portal.gamesparks.net/rest/games/44ujrQ3BnudG/mongo/preview/player/index

#### Example Response

```
[
{
    "v": 1,
    "key": {
      "_id": 1
    },
    "name": "_id_",
    "ns": "301604-game-preview.player"
  },
  {
    "v": 1,
    "unique": true,
    "key": {
      "userName": 1
    },
    "name": "userName_1",
    "ns": "301604-game-preview.player",
    "background": true
  },
  {
    "v": 1,
    "key": {
      "authTokens": 1
    },
    "name": "authTokens_1",
    "ns": "301604-game-preview.player",
    "background": true
  },
  {
    "v": 1,
    "key": {
      "userName": 1,
      "password": 1
    },
    "name": "userName_1_password_1",
    "ns": "301604-game-preview.player",
    "background": true
  }
 ]

```

## Errors

If an error occurs with any of the NoSQL Explorer REST API calls an error response will be returned containing a response code and a message.

```
{
 "responseCode": number,
 "errorMessage": string
}
```

#### Response Code Meanings


|Code   | Description  |
|---|---|
|-1   |General Error. See the error message for details.   |
|1   |The stage parameter must be either 'live' or 'preview'   |
|7   |Security error. Check the API key and Basic Auth credentials that you are using.   |
|8   |IO error. A failed or interrupted I/O operation has occurred.   |
