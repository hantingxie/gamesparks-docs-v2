---
src: /API Documentation/Cloud Code API/Cloud Data/SparkMongoCollectionReadWrite.md
---

# SparkMongoCollectionReadWrite

Provides read write only access to a mongo collection.

All methods defined in  SparkMongoCollectionReadOnly are available in this object along with those listed below.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var myMetaCollection = Spark.runtimeCollection('metatest');</pre>



## count
_signature_ count()</p>
_returns_ number</p>
Returns the number of documents in this collection<b>returns</b>the number of documents<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var count = myMetaCollection.count();</pre>


_signature_ count(JSON query)</p>
_returns_ number</p>
Returns the number of documents that match the supplied query<b>returns</b>the number of documents<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var count = Spark.metaCollection('metatest').count({"metafield" : "metavalue"});</pre>

## distinct
_signature_ distinct(string key)</p>
_returns_ JSON</p>
Returns a list of distinct values for the given key in the collection<b>params</b>key - the key to use in the query<b>returns</b>an object array<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var keys = Spark.metaCollection('metatest').distinct("metafield");</pre>


_signature_ distinct(string key, JSON query)</p>
_returns_ JSON</p>
Returns a list of distinct values for the given key in the collection that match the supplied query<b>params</b>key - the key to use in the queryquery - the Mongo query<b>returns</b>an object array<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var keys = Spark.metaCollection('metatest').distinct("metafield", {"metafield1":{"$gte" : 5}});</pre>

## dropIndex
_signature_ dropIndex(JSON keys)</p>
_returns_ void</p>
Drops or removes the specified index from a collection.<b>params</b>keys - the index definition used in ensureIndex.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').dropIndex({"metafield" : 1});</pre>

## dropIndexByName
_signature_ dropIndexByName(string name)</p>
_returns_ void</p>
Drops or removes the specified index from a collection.<b>params</b>name - the name of the index to drop.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').dropIndexByName("myIndex");</pre>

## ensureIndex
_signature_ ensureIndex(JSON keys)</p>
_returns_ void</p>
Creates an index on the specified fields if the index does not already exist.<b>params</b>keys - the index definition used in ensureIndex.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').ensureIndex({"metafield" : 1, "metafield1" : 1});</pre>


_signature_ ensureIndex(JSON keys, JSON optionsIN)</p>
_returns_ void</p>
Creates an index on the specified fields if the index does not already exist.<b>params</b>keys - the index definition used in ensureIndex.optionsIN - index options<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.metaCollection('metatest').ensureIndex({"metafield" : 1, "metafield1" : 1}, {"name":"myIndex"});</pre>

## find
_signature_ find()</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>
Returns a SparkMongoCursor of all documents in this collection<b>params</b><b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find();</pre>


_signature_ find(JSON query)</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>
Returns a SparkMongoCursor of all documents in this collection that match the supplied query<b>params</b>query - a Mongo query<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find({"metatest1" : {"$gt" : 1}});</pre>


_signature_ find(JSON query, JSON fields)</p>
_returns_ [SparkMongoCursor](/API Documentation/Cloud Code API/Cloud Data/SparkMongoCursor.md)</p>
Returns a SparkMongoCursor of all documents in this collection that match the supplied query.The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.<b>params</b>query -  a Mongo queryfields - the fields to return<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').find({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>

## findOne
_signature_ findOne()</p>
_returns_ JSON</p>
Returns the first document from the collection according to natural order (which reflects the order of documents on the disk)<b>returns</b>A JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var results = Spark.metaCollection('metatest').findOne();</pre>


_signature_ findOne(JSON query)</p>
_returns_ JSON</p>
Returns one document that satisfies the specified query criteria.If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.<b>params</b>query - a Mongo query<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}</pre>


_signature_ findOne(JSON query, JSON fields)</p>
_returns_ JSON</p>
Returns one document that satisfies the specified query criteria.If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.<b>params</b>query - a Mongo queryfields - the fields to return<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>


_signature_ findOne(JSON query, JSON fields, JSON orderBy)</p>
_returns_ JSON</p>
Returns one document that satisfies the specified query criteria.If multiple documents satisfy the query, this method returns the first document according to the natural order which reflects the order of documents on the disk.The returned documents only contain the fields supplied in the fieldsToReturn parameter. This reduces the document size when being returned.<b>params</b>query - a Mongo queryfields - the fields to returnorderBy - the order clause<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var result = Spark.metaCollection('metatest').findOne({"metatest1" : {"$gt" : 1}}, {"metatest" : 1});</pre>

## findAndModify
_signature_ findAndModify(JSON query, JSON update)</p>
_returns_ JSON</p>
Calls findAndModify(query, fields, sort, remove, update, returnNew, upsert) with fields=null, remove=false, returnNew=false, upsert=false, sort=null<b>params</b>query - Specifies the selection criteria for the modification. The query field employs the same query selectors as used in the find() method. Although the query may match multiple documents, findAndModify will only select one document to modify.update -  Must specify either the remove or the update field in the findAndModify command. The update field employs the same update operators or field: value specifications to modify the selected document.<b>returns</b>a JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var doc = myRuntimeCollection.findAndModify({"metafield" : "metavalue"}, {"metafield" : 1}, {"metafield" : "metavalue1"});</pre>


_signature_ findAndModify(JSON query, JSON sort, JSON update)</p>
_returns_ JSON</p>
Calls findAndModify(query, fields, sort, remove, update, returnNew, upsert) with fields=null, remove=false, returnNew=false, upsert=false<b>params</b>query - Specifies the selection criteria for the modification. The query field employs the same query selectors as used in the find() method. Although the query may match multiple documents, findAndModify will only select one document to modify.sort - Determines which document the operation will modify if the query selects multiple documents. findAndModify will modify the first document in the sort order specified by this argument.update -  Must specify either the remove or the update field in the findAndModify command. The update field employs the same update operators or field: value specifications to modify the selected document.<b>returns</b>a JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var doc = myRuntimeCollection.findAndModify({"metafield" : "metavalue"},{"metafield" : 1}, {"metafield" : "metavalue1"});</pre>


_signature_ findAndModify(JSON query, JSON fields, JSON sort, boolean remove, JSON update, boolean returnNew, boolean upsert)</p>
_returns_ JSON</p>
Atomically modifies and returns a single document. By default, the returned document does not include the modifications made on the update. To return the document with the modifications made on the update, use the returnNew option.<b>params</b>query - specifies the selection criteria for the modification. The query field employs the same query selectors as used in the find() method. Although the query may match multiple documents, findAndModify will only select one document to modify.fields - the fields to returnsort - determines which document the operation will modify if the query selects multiple documents. findAndModify will modify the first document in the sort order specified by this argument.remove - must specify either the remove or the update field in the findAndModify command. When true, removes the selected document. The default is false.update -  must specify either the remove or the update field in the findAndModify command. The update field employs the same update operators or field: value specifications to modify the selected document.returnNew - when true, returns the modified document rather than the original. The findAndModify method ignores the new option for remove operations. The default is false.upsert - used in conjunction with the update field. When true, the findAndModify command creates a new document if the query returns no documents. The default is false.<b>returns</b>a JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var doc = myRuntimeCollection.findAndModify({"metafield" : "metavalue"},{"metafield" : 1},false,{"metafield" : "metavalue1"},true, {"metafield" : 1},false);</pre>

## findAndRemove
_signature_ findAndRemove(JSON query)</p>
_returns_ JSON</p>
Calls findAndModify(query, fields, sort, remove, update, returnNew, upsert) with  fields=null, sort=null, remove=true, returnNew=false, upsert=false<b>params</b>query - a Mongo query<b>returns</b>a JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var doc = myRuntimeCollection.findAndRemove({"metafield" : "metavalue"});</pre>

## insert
_signature_ insert(JSON[] documents)</p>
_returns_ boolean</p>
Inserts a document or documents into a collection.<b>params</b>documents - A document or array of documents to insert into the collection.<b>returns</b>true if the operation was successful<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.insert({"metafield" : "metavalue"}, {"metafield" : "metavalue1"}, {"metafield" : "metavalue2"});</pre>

## aggregate
_signature_ aggregate(JSON firstOp, JSON[] additionalOps)</p>
_returns_ JSON</p>


## applyChanges
_signature_ applyChanges(JSON existingDocument, JSON newDocument)</p>
_returns_ boolean</p>
Generates the correct mongo update command to set and unset fields so the mongo record matches the newDocument.This can greatly increase performance in documents where only a small amount of change has been made as only the required fields are modified.If the existing document is null, the new document is inserted directly into the collection<b>params</b>existingDocument - A document perviously retrieved from the database. The _id field of this document will be used to determine which document to update. If the document passed has no _id the call will fail.newDocument - The new state to persist in the database, and _id field in this document will be ignored.<b>returns</b>true if the operation was successful

## getIndexInfo
_signature_ getIndexInfo()</p>
_returns_ JSON</p>
Return a list of the indexes for this collection. Each object in the list is the "info document" from MongoDB<b>returns</b>list of index documents<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var indexes = Spark.metaCollection('metatest').getIndexInfo();</pre>

## getLastError
_signature_ getLastError()</p>
_returns_ JSON</p>
Gets the error (if there is one) from the previous operation on this connection.<b>returns</b>a JSON object with error and status information<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var errors = Spark.metaCollection('metatest').getLastError();</pre>

## save
_signature_ save(JSON document)</p>
_returns_ boolean</p>
Updates an existing document or inserts a new document, depending on its document parameter.If the document does not contain an _id field, then the save() method performs an insert. During the operation, mongo will add to the document the _id field and assign it a unique ObjectId.If the document contains an _id field, then the save() method performs an upsert, querying the collection on the _id field. If a document does not exist with the specified _id value, the save() method performs an insert. If a document exists with the specified _id value, the save() method performs an update that replaces all fields in the existing document with the fields from the document.<b>params</b>document - the document to save<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.save({"metafield" : "metavalue"});</pre>

## remove
_signature_ remove(JSON query)</p>
_returns_ boolean</p>
Removes any document from the collection that matches the supplied query.Return a boolean indicating whether the remove was successful.<b>params</b>query - the query<b>returns</b>true if the operation was successful<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.remove({"metafield" : "metavalue"});</pre>

## drop
_signature_ drop()</p>
_returns_ void</p>
Drop the collection<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">myRuntimeCollection.drop();</pre>

## update
_signature_ update(JSON query, JSON update)</p>
_returns_ boolean</p>
Calls update(query, update, upsert, multi) with upsert=false and multi=false<b>params</b>query - query (document) The selection criteria for the update. Use the same query selectors as used in the find() methodupdate - update (document) The modifications to apply. For details see Update Parameter<b>returns</b>true if the operation was successful<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.update({"metafield" : "metavalue"}, {"metafield" : "metavalue1"});</pre>


_signature_ update(JSON query, JSON update, boolean upsert, boolean multi)</p>
_returns_ boolean</p>
Modifies an existing document or documents in a collection. The method can modify specific fields of existing document or documents or replace an existing document entirely, depending on the update parameter.By default, the update() method updates a single document. If the multi option is set to true, the method updates all documents that match the query criteria.<b>params</b>query - query (document) The selection criteria for the update. Use the same query selectors as used in the find() methodupdate - update (document) The modifications to apply. For details see Update Parameterupsert - if set to true, creates a new document when no document matches the query criteria. The default value is false, which does not insert a new document when no match is foundmulti - multi (boolean) Optional. If set to true, updates multiple documents that meet the query criteria. If set to false, updates one document. The default value is false. For additional information, see Multi Parameter<b>returns</b>true if the operation was successful<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.update({"metafield" : "metavalue"}, {"metafield" : "metavalue1"}, false, false);</pre>

## updateMulti
_signature_ updateMulti(JSON query, JSON update)</p>
_returns_ boolean</p>
Calls update(query, update, upsert, multi) with upsert=false and multi=true<b>params</b>query - query (document) The selection criteria for the update. Use the same query selectors as used in the find() methodupdate - update (document) The modifications to apply. For details see Update Parameter<b>returns</b>true if the operation was successful<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var success = myRuntimeCollection.updateMulti({"metafield" : "metavalue"}, {"metafield" : "metavalue1"});</pre>

