# SparkRealtimeServer

Provides the details of the realtime server on which a match will be played out

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var server = Spark.getMultiplayer().loadMatch(matchId).getServer();</pre>



## getHost

_signature_ getHost()</p>

_returns_ string</p>

<b>validity</b> All Scripts

<b>returns</b>

The hostname of the server

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var host = server.getHost()</pre>


## getPort

_signature_ getPort()</p>

_returns_ number</p>

<b>validity</b> All Scripts

<b>returns</b>

The port to connect to on the server

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var port = server.getPort()</pre>


