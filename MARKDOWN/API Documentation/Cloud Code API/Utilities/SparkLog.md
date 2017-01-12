# SparkLog

A Logging interface that can be called from scripts.
This interface writes to the script.log table that is accessible in the developer portal using the NoSQL explorer tool.
The object passed can either be complex JSON or simple javascript values.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var logger = Spark.getLog();</pre>

## debug
_signature_ debug(JSON msg)</p>
_returns_ void</p>

Records value into the spark.log table with the level set to debug.
<b>params</b>
msg - the message to log
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().debug("Simple string logging");</pre>
## info
_signature_ info(JSON msg)</p>
_returns_ void</p>

Records value into the spark.log table with the level set to info.
<b>params</b>
msg - the message to log
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().info({type:"JSON logging"});</pre>
## warn
_signature_ warn(JSON msg)</p>
_returns_ void</p>

Records value into the spark.log table with the level set to warn.
<b>params</b>
msg - the message to log
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().warn({type:"JSON logging"})</pre>
## error
_signature_ error(JSON msg)</p>
_returns_ void</p>

Records value into the spark.log table with the level set to info.
<b>params</b>
msg - the message to log
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().error({type:"JSON logging"})</pre>
## getLevel
_signature_ getLevel()</p>
_returns_ string</p>

Returns the currently configured log level.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().getLevel()</pre>
## setLevel
_signature_ setLevel(string level)</p>
_returns_ void</p>

Updates the current level that logs will be written at.
Entries will only be written if the level is greater than the current level set.
Available levels are: "DEBUG", "INFO", "WARN", "ERROR".
Note: this change takes time to propagate throughout the system, it may be minutes before all servers are using the new level.
<b>params</b>
level - the new level at which to log
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLog().setLevel("DEBUG")</pre>
