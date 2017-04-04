---
src: /API Documentation/Cloud Code API/Multiplayer/SparkMatch.md
---

# SparkMatch

Provides access to a match's details.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var match = Spark.getMultiplayer().loadMatch(matchId);</pre>



## getId

_signature_ getId()</p>

_returns_ string</p>

<b>validity</b> All Scripts

<b>returns</b>

The id of this match

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = match.getId()</pre>


## getParticipants

_signature_ getParticipants()</p>

_returns_ [SparkParticipant](/API Documentation/Cloud Code API/Multiplayer/SparkParticipant.md)[]</p>

<b>validity</b> All Scripts

<b>returns</b>

An array containing all of the participants of this match

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var participant = match.getParticipants()</pre>


## getServer

_signature_ getServer()</p>

_returns_ [SparkRealtimeServer](/API Documentation/Cloud Code API/Multiplayer/SparkRealtimeServer.md)</p>

<b>validity</b> All Scripts

<b>returns</b>

The details of the realtime server on which this match will take place.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var server = match.getServer()</pre>


## addPlayers

_signature_ addPlayers([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Add the given players to this match.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.addPlayers(playersToAdd)</pre>


## addPlayersById

_signature_ addPlayersById(string[] playerIds)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Add the players with the given playerIds to this match.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.addPlayersById(playerIdsToAdd)</pre>


## removePlayers

_signature_ removePlayers([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Remove the given players from this match.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.removePlayers(playersToRemove)</pre>


## removePlayersById

_signature_ removePlayersById(string[] playerIds)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Remove the players with the given playerIds from this match.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.removePlayersById(playerIdsToRemove)</pre>


## enableRealtime

_signature_ enableRealtime(string script)</p>

_returns_ void</p>

<b>validity</b> All Scripts

If this match is not already realtime enabled, this method will enabled realtime.

The realtime servers for this match will be configured to use the realtime script provided

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.enableRealtime('MY_RT_SCRIPT');</pre>


_signature_ enableRealtime()</p>

_returns_ void</p>

<b>validity</b> All Scripts

If this match is not already realtime enabled, this method will enabled realtime.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.enableRealtime();</pre>


## getMatchData

_signature_ getMatchData()</p>

_returns_ JSON</p>

<b>validity</b> All Scripts

Returns the matchData for the match instance.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.getMatchData();</pre>


## isRealtimeEnabled

_signature_ isRealtimeEnabled()</p>

_returns_ boolean</p>

<b>validity</b> All Scripts

Whether this match has realtime servers enabled.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var isEnabledForRealtime = match.isRealtimeEnabled();</pre>


## setMatchData

_signature_ setMatchData(JSON matchData)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Sets the matchData for the match instance.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">match.setMatchData(matchData);</pre>


