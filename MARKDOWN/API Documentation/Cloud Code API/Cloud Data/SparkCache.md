# SparkCache

Provides the ability to cache javascript objects. This includes complex objects with functions. Any javascript object can be cached. This allows you to create objects of a particular structure from your JSON data in mongo that can speed up access.
This differs slighty from storing data in mongo as the data is stored in memory and expired on a LRU basis. This means access time is significantly faster for these in memory objects
Cached objects are backed by mongo, so if an item is expired, when you try to access it again it will be reloaded.
There is a limited amount of memory available on servers, so this should be used for few, shared configuration type objects
Using this for player data or having a large amount of objects could slow down you application as the store / reload process is more expensive than a mongo find for JSON data
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var theCache = Spark.getCache();</pre>


## put

_signature_ put(string key, JSON object)</p>
_returns_ void</p>

Adds an object to the cache
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">theCache.put("key", myObject);</pre>

## get

_signature_ get(string key)</p>
_returns_ JSON</p>

Gets an objects from the cache
<b>returns</b>
A JavaScipt object, or null depending on whether put has ben called for the given key 
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var myObject = theCache.get("key");</pre>

## remove

_signature_ remove(string key)</p>
_returns_ void</p>

Remove an object from the cache
The object will be removed form the cache, and form the database. Subsequent calls to get will return null
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false"> theCache.remove("key")</pre>

## removeAll

_signature_ removeAll()</p>
_returns_ void</p>

Clears everything from the cache
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false"> theCache.removeAll()</pre>

_signature_ removeAll(string pattern)</p>
_returns_ void</p>

Clears all objects from the cache where the keys match the regex pattern provided.
the match pattern is ultimately used by mongo to do a $regex query, which uses
"Perl Compatible Regular Expressions" (PCRE) as the matching engine.
<pre rel="highlighter" code-brush="js" contenteditable="false"> theCache.removeAll("match\..*\.2014)</pre>
