---
nav_sort: 6
src: /Tutorials/Database Access and Cloud Storage/Basic NoSQL Retrieval and Persistence.md
---

# Basic NoSQL Retrieval and Persistence

When you need to store custom data in your game, you will usually want to store this in a runtime collection (but see [Managing Data Persistence](/Tutorials/Database Access and Cloud Storage/Managing Data Persistence.md) for other options).

This tutorial lays out some important guidelines for working with and managing runtime collections in the GameSparks platform using basic NoSQL retrieval and persistence methods.

## Storing Data and the Collection ID

Before storing or retrieving any data, you first need a reference to the database collection. This is achieved as follows:

```
var collection = Spark.runtimeCollection("myCustomCollection");

```

Once you have access to the collection, you can store your custom data in it as follows:

```
var customData = {"key": "value"};
collection.save(customData);

```

Note that every document in a collection is identified by a unique identifier, keyed as *\_id* in the document.

We didn’t explicitly define an *\_id* field in our data, so the database creates one for us automatically when the document is created in the database. Generally, allowing the database to assign one is the recommended method for generating an ID for your documents, although you can explicitly define it yourself if you need to.

<q>**Note: Collections are automatically created.** If the collection doesn’t already exist, it's created automatically for you the first time you try to save data into it. There is no need to explicitly create a collection at any point in time.</q>

<q>**Warning: IDs must be unique!** IDs in a collection must be unique, so if you generate them yourself, be certain your algorithm to generate these produces unique values every time. A typical example of this would be to use the player’s ID to store extra data for the player in your own collection. You can use the same ID across different collections – IDs must only be unique within the same collection.</q>



### Retrieving the Collection ID

If you've allowed the database to automatically assign an ID to your document, the data you saved will now have an extra field *\_id*, for example:

```
var documentId = customData._id;

```

This way you can retrieve the ID for the new document so that the data can be retrieved later. You can also retrieve data by searching on any other fields in the data, but retrieving by ID is the fastest and most efficient way, so is recommended whenever possible.

<q>**Note:** Once the data has been saved to the database, the generated *\_id* is automatically added to your JSON data in-memory. You don’t need to retrieve the data from the database again in order to find this ID, you can simply get it from the JSON object as shown above.</q>

### Understanding and Retrieving ObjectID (OID)

IDs assigned automatically are not simple numbers or strings, but are a special type of data known as an ObjectID (or OID for short). If you want the string representation of the OID (which is fairly common if you want to pass this back to the client, for example) you can get this as follows:

```
var documentIdStr = customData._id.$oid;

```

## Updating Documents in a Collection

In order to update this document, you use the update command as follows:

```
var query = {"_id": {"$oid": "57fe0b4a3a32df048bf27405"}};
var update = {"key":"value2"};
collection.update(query, update);

```

In this example, the entire document would be replaced by the new version given by the update parameter.

Normally, you wouldn’t want to replace the entire document – often you just want to update a single field on the document. In this case, you could do something like:

```
var query = {"_id": {"$oid": "57fe0b4a3a32df048bf27405"}};
var update = {"$set":{"key":"onlyThisFieldIsUpdated"}};
collection.update(query, update);

```
</br>
### Using "upsert" and "multi" when Updating

Updates also support two additional parameters: *upsert* and *multi*:
* The *upsert* parameter allows a new document to be inserted (as opposed to an existing one being updated) if no existing document is found.
* The *multi* parameter allows multiple documents to be updated with a single command (by default, only the first document that matches the query is updated unless this is specified).

So to perform an upsert for a single document, set the *upsert* parameter (the third parameter) to be true:

```
collection.update(query, update, true, false);

```

And to update multiple documents (assuming that more than one document matches the query), set the *multi* parameter (the fourth parameter) to be true:

```
collection.update(query, update, false, true);

```

## Retrieving Data from the Database


To retrieve data from the database, you use one of the available *find()* methods.

### Retrieving a Single Document

If you want to retrieve a specific document, you can use a variant of the *findOne()* command. So, if you had a document in your collection which looked like this:

```
{
 "_id": {
  "$oid": "57fe0b4a3a32df048bf27405"
 },
 "key": "value"
}

```

You could retrieve this data in Cloud Code as follows:

```
var retrievedData = collection.findOne( {"_id": {"$oid":"57fe0b4a3a32df048bf27405"}} );

```

Note the *{"$oid":"57fe0b4a3a32df048bf27405"}* value for the *\_id* field. *$oid* is an extension to the standard JSON format to allow conversion from strings to database ObjectIDs. If you had the original variable (which is already in ObjectID format) you wouldn’t need to do this conversion, for example:

```
var retrievedData = collection.findOne({"_id": documentId});

```

This returns a JSON object, which will be identical to the one you saved previously.

### Retrieving Multiple Documents

Sometimes you don’t want to retrieve just a single document, but a range of documents matching some criteria. For example, you might have a runtime collection called "age" which stores player ages with documents that look as follows:

```

{ "_id": { "$oid": "57fe0c353a32df048bf281ec" }, "age":35, "name":"Bob" }
{ "_id": { "$oid": "57fe0dcd3a32df048bf29a2e" }, "age":43, "name":"Alice" }
and so on...

```

In this case, you might want to retrieve documents where the age is 35:

```
var cursor = collection.find( {"age":35} );

```

Note that unlike *findOne()*, the *find()* command doesn’t return a single document, but a cursor which allows you to iterate over the results:

```

while (cursor.hasNext()) {
    var doc = cursor.next();
    // Do something with each document here…
}

```

<q>**Warning: Excessive Memory Load!** Be careful about the queries you use when retrieving data in this way. If you retrieve more data than you really need, you will load a lot of data from the database into memory, which will slow down the performance of your game.</q>

## Controlling Data Retrieval

### Specifying Fields Returned

You can limit the amount of data retrieved by specifying which fields you want returned. In the above example, we already know that the "age" field will be 35 for all the returned documents (because that’s what we searched for). All we really want are the IDs of the documents (which might, for example, represent player IDs). In this case, we can ask for only the data we want as follows:

```

var cursor = collection.find( {"age":35}, {"_id":1} );

```
Here:
* The first parameter is still the query to identify the data we want to retrieve.
* The second parameter specifies which fields we want to retrieve from those documents.

In this case, we specify that we want the *\_id* field by giving it a value of 1. If we do this, the database assumes that (because we specified which field we want) the other fields are not required. So this query would return a cursor containing documents like this:

```

{ "_id": { "$oid": "57fe0c353a32df048bf281ec" } }

```


If we wanted all the fields except the age field, we would pass in:

```

var cursor = collection.find( {"age":35}, {"age":0} );

```

In this case, the value of 0 indicates we don’t want that field (the other fields are returned by default) and would return a cursor containing documents like:

```

{ "_id": { "$oid": "57fe0c353a32df048bf281ec" }, "name":"Bob" }

```

You can specify as many fields as you need in this parameter (each with a value of 0 or 1) to specify the exact fields you require.

### Ordering Returned Documents

If you are retrieving multiple documents, you may want them retrieved in a particular order. You can specify a sort order on the cursor object:

```

var cursor = collection.find( {"age":35} ).sort( {"_id":1} );

```

This would sort the returned data in order of ascending *\_id* field.

To sort in descending order, specify -1 as the value:

```

var cursor = collection.find( {"age":35} ).sort( {"_id":-1} );

```

Again, you can specify as many fields as you need in the sort parameter, in order to sort by multiple fields.

### Limiting Documents Returned

Often, you want to limit the number of documents returned by a cursor. This is a simple operation:

```

var cursor = collection.find( {"age":35} ).limit(10);

```

This would return the first 10 documents found on the database, and no more.

### Skipping Documents Returned

Finally, it's possible to skip documents returned by a cursor. If you wanted to skip the first 10 documents, you could use:

```

var cursor = collection.find( {"age":35} ).sort( {"_id":-1} ).skip(20).limit(10);

```

In this case, the data would be sorted by *\_id* first, then the first 20 documents are skipped. Reading from the cursor would now return data from the 21st – 30th documents (because we also limited to returning 10 documents).

<q>**Warning: Processing Overheads!**  Using the *skip()* command can be a relatively expensive operation. If, for example, you planned to use this to implement a paging system for retrieving data, be aware that skipping the data has nearly as much overhead as reading the data from the cursor, so can be slow for large datasets.</q>

A better method to implement paging would be to sort by a field such as *\_id*, and retrieve the first "page" of data using a *limit(10)*. Then, remember the ID of the last document, and to retrieve the next page, query for documents where the *\_id* is greater than the last one you retrieved (in addition to your normal query constraints), for example:

```

var cursor = collection.find( {"age": 35, "_id": {"$gt": {"$oid": "57fe0b4a3a32df048bf27405"}}} ).sort({"_id":1}).limit(10);

```
</br>
<q>**Note: Perform cursor operations first!** Cursor operations such as *sort()*, *limit()*, and *skip()* should be performed before any data is read from the cursor.
