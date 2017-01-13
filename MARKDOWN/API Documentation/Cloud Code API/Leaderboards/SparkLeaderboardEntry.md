---
src: /API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardEntry.md
---

# SparkLeaderboardEntry

An entry within a leaderboard.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var entry = leaderboard.getEntries().next();</pre>

## getUserId
_signature_ getUserId()</p>
_returns_ string</p>

Returns the playerId of the player whose entry in the leaderboard this is.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var playerId = entry.getUserId();</pre>
## getUserName
_signature_ getUserName()</p>
_returns_ string</p>

Returns the displayName of the player whose entry in the leaderboard this is.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var displayName = entry.getUserName();</pre>
## getRank
_signature_ getRank()</p>
_returns_ number</p>

Returns the position of this entry within the leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var rank = entry.getRank();</pre>
## getRankPercentage
_signature_ getRankPercentage()</p>
_returns_ number</p>

Returns the rank of the player as a percentage of total entries.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var rankPercentage = entry.getRankPercentage();</pre>
## getWhen
_signature_ getWhen()</p>
_returns_ string</p>

Returns a String representing the time this entry was recorded, in the format yyyy-MM-dd'T'HH:mm'Z'.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var when = entry.getWhen();</pre>
## getAttribute
_signature_ getAttribute(string name)</p>
_returns_ JSON</p>

Returns the attribute <b>name</b> from this leaderboard entry.  Use this to get custom attributes from this entry.
<b>params</b>
name - the name of the attribute to be returned
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var score = entry.getAttribute("SCORE");</pre>
