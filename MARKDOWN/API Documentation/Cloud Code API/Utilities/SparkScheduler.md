# SparkScheduler

Utility to schedule execution of a module in the future
<b>validity</b> All Scripts
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var theScheduler = Spark.getScheduler();</pre>


## inSeconds

_signature_ inSeconds(string shortCode, number delaySeconds, JSON data)</p>
_returns_ boolean</p>

Schedules the execution of the supplied module. The scheduled script will run in the context of the current player
<b>params</b>
shortCode - The shortCode of the module to execute
delaySeconds - How long to wait until executing the module
data - The data to pass to the module. This will be available as Spark.getData() when the module is running
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">theScheduler.inSeconds("SHORT_CODE", 15, {"myData" : myData});</pre>

_signature_ inSeconds(string shortCode, number delaySeconds, JSON data, string key)</p>
_returns_ boolean</p>

Schedules the execution of the supplied module
<b>params</b>
shortCode - The shortCode of the module to execute
delaySeconds - How long to wait until executing the module
data - The data to pass to the module. This will be available as Spark.getData() when the module is running
key - The id of the scheduled item. If schedule already exists for the given key it's details will be updated
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">theScheduler.inSeconds("SHORT_CODE", 15, {"myData" : myData}, "logTimeout-" + Spark.getPlayer().getPlayerId());</pre>

## cancel

_signature_ cancel(string key)</p>
_returns_ void</p>

Cancels the execution of a previously scheduled module.
<b>params</b>
key - The id of the scheduled item to cancel.
