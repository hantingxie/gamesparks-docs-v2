# SparkProperties

Provides access to the properties for the current game.
<pre rel="highlighter" code-brush="js" contenteditable="false">var properties = Spark.getProperties();</pre>

## getProperty
_signature_ getProperty(string propertyShortCode)</p>
_returns_ JSON</p>

Returns the property with the given shortCode, as JSON
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var property = Spark.getProperties().getProperty(propertyShortCode);</pre>
## getPropertySet
_signature_ getPropertySet(string propertySetShortCode)</p>
_returns_ JSON</p>

Returns the property set with the given shortCode, as JSON
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var propertySet = Spark.getProperties().getPropertySet(propertySetShortCode);</pre>
