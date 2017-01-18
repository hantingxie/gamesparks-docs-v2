---
src: /API Documentation/Cloud Code API/Cloud Data/SparkMongoCollectionReadOnly.md
---

# SparkMongoCollectionReadOnly

Provides read only access to a mongo collection.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var myMetaCollection = Spark.metaCollection('metatest');</pre>


## count

_signature_ count()</p>
_returns_ number</p>

Returns the number of documents in this collection
<b>returns</b>
the number of documents
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var count = myMetaCollection.count();</pre>

_signature_ count(JSON query)</p>
_returns_ number</p>

Returns the number of documents that match the supplied query
<b>returns</b>
the number of documents
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var count = Spark.metaCollection('metatest').count({"metafield" : "metavalue"});</pre>

## distinct

_signature_ distinct(string key)</p>
_returns_ JSON</p>

Returns a list of distinct values for the given key in the collection
<b>params</b>
key - the key to use in the query
<b>returns</b>
an object array
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var keys = Spark.metaCollection('metatest').distinct("metafield");</pre>

_signature_ distinct(string key, JSON query)</p>
_returns_ JSON</p>

Returns a list of distinct values for the given key in the collection that match the supplied query
<b>params</b>
key - the key to use in the query
query - the Mongo query
<b>returns</b>
an object array
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var keys = Spark.metaCollection('metatest').distinct("metafield", {"metafield1":{"$gte" : 5}});</pre>

## dropIndex

_signature_ dropIndex(JSON keys)</p>
_returns_ void</p>

Drops or removes the specified index from a collection.
<b>params</b>
keys - the index definition used in ensureIndex.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').dropIndex({"metafield" : 1});</pre>

## dropIndexByName

_signature_ dropIndexByName(string name)</p>
_returns_ void</p>

Drops or removes the specified index from a collection.
<b>params</b>
name - the name of the index to drop.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').dropIndexByName("myIndex");</pre>

## ensureIndex

_signature_ ensureIndex(JSON keys)</p>
_returns_ void</p>

Creates an index on the specified fields if the index does not already exist.
<b>params</b>
keys - the index definition used in ensureIndex.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').ensureIndex({"metafield" : 1, "metafield1" : 1});</pre>

_signature_ ensureIndex(JSON keys, JSON optionsIN)</p>
_returns_ void</p>

Creates an index on the specified fields if the index does not already exist.
<b>params</b>
keys - the index definition used in ensureIndex.
optionsIN - index options
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').ensureIndex({"metafield" : 1, "metafield1" : 1}, {"name":"myIndex"});</pre>

## find

_signature_ find()</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>

Returns a SparkMongoCursor of all documents in this collection
<b>params</b>
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find();</pre>

_signature_ find(JSON query)</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>

Returns a SparkMongoCursor of all documents in this collection that match the supplied query
<b>params</b>
query - a Mongo query
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find({"metatest1" : {"$gt" : 1}});</pre>

_signature_ find(JSON query, JSON fields)</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>

Returns a SparkMongoCursor of all documents in this collection that match the supplied query.
The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.
<b>params</b>
query -  a Mongo query
fields - the fields to return
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>

## findOne

_signature_ findOne()</p>
_returns_ JSON</p>

Returns the first document from the collection according to natural order (which reflects the order of documents on the disk)
<b>returns</b>
A JSON object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').findOne();</pre>

_signature_ findOne(JSON query)</p>
_returns_ JSON</p>

Returns one document that satisfies the specified query criteria.
If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.
<b>params</b>
query - a Mongo query
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}</pre>

_signature_ findOne(JSON query, JSON fields)</p>
_returns_ JSON</p>

Returns one document that satisfies the specified query criteria.
If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.
The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.
<b>params</b>
query - a Mongo query
fields - the fields to return
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>

_signature_ findOne(JSON query, JSON fields, JSON orderBy)</p>
_returns_ JSON</p>

Returns one document that satisfies the specified query criteria.
If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.
The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.
<b>params</b>
query - a Mongo query
fields - the fields to return
orderBy - the order clause
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>

## aggregate

_signature_ aggregate(JSON firstOp, JSON[] additionalOps)</p>
_returns_ JSON</p>



## getIndexInfo

_signature_ getIndexInfo()</p>
_returns_ JSON</p>

Return a list of the indexes for this collection. Each object in the list is the "info document" from MongoDB
<b>returns</b>
list of index documents
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var indexes = Spark.metaCollection('metatest').getIndexInfo();</pre>

## getLastError

_signature_ getLastError()</p>
_returns_ JSON</p>

Gets the error (if there is one) from the previous operation on this connection.
<b>returns</b>
a JSON object with error and status information
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var errors = Spark.metaCollection('metatest').getLastError();</pre>
