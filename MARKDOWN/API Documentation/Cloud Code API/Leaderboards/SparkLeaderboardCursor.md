---
src: /API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardCursor.md
---

# SparkLeaderboardCursor

A cursor over entries within a leaderboard.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getLeaderboard(shortCode).getEntries();</pre>


## hasNext
_signature_ hasNext()</p>
_returns_ boolean</p>

Returns true if there are more entries available.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var hasNext = cursor.hasNext();</pre>

## next
_signature_ next()</p>
_returns_ [SparkLeaderboardEntry](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardEntry.md)</p>

Returns the entry the cursor is at and moves the cursor ahead by one.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var entry = cursor.next();</pre>

