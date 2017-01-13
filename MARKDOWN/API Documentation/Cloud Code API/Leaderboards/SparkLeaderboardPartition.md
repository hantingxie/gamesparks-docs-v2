---
src: /API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardPartition.md
---

# SparkLeaderboardPartition

Represents a single partition of a leaderboard.  A partition is also a SparkLeaderboard and can be used wherever a SparkLeaderboard is used.
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var partition = Spark.getLeaderboards().getLeaderboard(shortCode).getPartitions()[0];</pre>

## getDescription
_signature_ getDescription()</p>
_returns_ string</p>

Returns the description of this leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var desc = Spark.getLeaderboards().getLeaderboard(shortCode).getDescription();</pre>
## getName
_signature_ getName()</p>
_returns_ string</p>

Returns the name of this leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var shortCode = Spark.getLeaderboards().getLeaderboard(shortCode).getName();</pre>
## getShortCode
_signature_ getShortCode()</p>
_returns_ string</p>

Returns the shortCode of this leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var shortCode = Spark.getLeaderboards().getLeaderboard(shortCode).getShortCode();</pre>
## getEntryCount
_signature_ getEntryCount()</p>
_returns_ number</p>

Returns the total number of entries in this leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var count = Spark.getLeaderboards().getLeaderboard(shortCode).getEntryCount();</pre>
## getEntryCountForIdentifier
_signature_ getEntryCountForIdentifier(string identifier)</p>
_returns_ number</p>

Returns the total number of entries in this leaderboard for the specified identifier.
The later can be the userId of a player or the id of a team.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var count = Spark.getLeaderboards().getLeaderboard(shortCode).getEntryCountForIdentifier("myPlayerId");</pre>
## getEntries
_signature_ getEntries()</p>
_returns_ [SparkLeaderboardCursor](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardCursor.md)</p>

Returns a cursor over all the entries in this leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var cursor = Spark.getLeaderboards().getLeaderboard(shortCode).getEntries();</pre>

_signature_ getEntries(number count, number offset)</p>
_returns_ [SparkLeaderboardCursor](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardCursor.md)</p>

Returns a cursor over <b>count</b> entries in this leaderboard, starting at <b>offset</b>.
<b>params</b>
count - the number of entries over which to obtain a cursor.
offset - the number of entries to skip before the start of the cursor.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var cursor = Spark.getLeaderboards().getLeaderboard(shortCode).getEntries(mycount, myoffset);</pre>
## isPartitioned
_signature_ isPartitioned()</p>
_returns_ boolean</p>

Returns true if this leaderboard has or can have partitions.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var isPartitioned = Spark.getLeaderboards().getLeaderboard(shortCode).isPartitioned();</pre>
## isPartition
_signature_ isPartition()</p>
_returns_ boolean</p>

Returns true if this leaderboard is a single partition of a parent leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var isPartitioned = Spark.getLeaderboards().getLeaderboard(shortCode).isPartition();</pre>
## getPartitions
_signature_ getPartitions()</p>
_returns_ [SparkLeaderboardPartition](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardPartition.md)[]</p>

Returns an array containing the partitions of this leaderboard if it is partitioned, otherwise an empty array is returned.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var partitions = Spark.getLeaderboards().getLeaderboard(shortCode).getPartitions();</pre>
## drop
_signature_ drop()</p>
_returns_ void</p>

Deletes this leaderboard partition, removing it from the parent leaderboard and deleting the underling leaderboard data for this partition.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLeaderboards().getLeaderboard(shortCode).getPartitions()[0].drop();</pre>

_signature_ drop(boolean deleteRunningTotalData)</p>
_returns_ void</p>

See #drop.  Additionally deletes the underlying running total data, resetting any record of players' scores.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.drop(true);</pre>
## archive
_signature_ archive()</p>
_returns_ void</p>

Archives this leaderboard partition.  Players will no longer be able to post new scores to this leaderboard, but the leaderboard is still available to view.
If the leaderboard partition has already been archived calling this has no effect.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLeaderboards().getLeaderboard(shortCode).getPartitions()[0].archive();</pre>
## isArchived
_signature_ isArchived()</p>
_returns_ boolean</p>

Returns true if this partition has been archived.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getLeaderboards().getLeaderboard(shortCode).getPartitions()[0].isArchived();</pre>
## getEntriesForIdentifier
_signature_ getEntriesForIdentifier(string identifier, JSON customIdFilter)</p>
_returns_ SparkLeaderboardEntry[]</p>

Returns the array of leaderboard entries that correspond to the supplied identifier and customIdFilter
If the customIdFilter is null, the method returns all the entries in the leaderboard for the suplied identifier
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.getEntriesForIdentifier(myPlayerId, {});</pre>
## getEntriesFromPlayer
_signature_ getEntriesFromPlayer(string playerId, number count)</p>
_returns_ [SparkLeaderboardCursor](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardCursor.md)</p>

Returns a cursor over the leaderboard entries starting from the highest score of the supplied playerId
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.getEntriesFromPlayer(myPlayerId, 50);</pre>
## getEntriesFromPlayerForCustomId
_signature_ getEntriesFromPlayerForCustomId(string playerId, number count, JSON customIdFilter)</p>
_returns_ [SparkLeaderboardCursor](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardCursor.md)</p>

Returns a cursor over the leaderboard entries starting from the highest score of the supplied playerId and customIdFilter
If the customId filter is not an object with valid ID fields, it will return an empty cursor
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.getEntriesFromPlayerForCustomId(myPlayerId, 50, {carType:"raceCar"});</pre>
## getIdFields
_signature_ getIdFields()</p>
_returns_ string[]</p>

Returns the list of custom ID fields that are defined on the leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.getIdFields();</pre>
## getScoreFields
_signature_ getScoreFields()</p>
_returns_ string[]</p>

Returns the list of fields that are defined on the leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.getScoreFields();</pre>
## deleteAllEntries
_signature_ deleteAllEntries(string identifier, boolean deleteRunningTotals)</p>
_returns_ boolean</p>

Deletes all entries from the leaderboard that correspond to this identifier. If your leaderboard has custom IDs set up, 
it will delete the entries for all the custom IDs
This method only works for realtime leaderboards
If deleteRunningTotals is true, all running total data for these entries will also be deleted
deleting running totals may affect other leaderbaords using the same running totals
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.deleteEntry(myPlayerId, true);</pre>
## deleteEntriesForCustomId
_signature_ deleteEntriesForCustomId(string identifier, boolean deleteRunningTotals, JSON customIdFilter)</p>
_returns_ boolean</p>

Deletes the entries from the leaderboard that match the specified customIdFilter.
This method only works for realtime leaderboards
If deleteRunningTotals is true, all running total data for this leaderboard will also be deleted
deleting running totals may affect other leaderbaords using the same running totals
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.deleteEntriesForCustomId(myPlayerId, true, {"carType":"raceCar"});</pre>
## deleteEntry
_signature_ deleteEntry(string identifier, boolean deleteRunningTotals)</p>
_returns_ boolean</p>

<b>DEPRECATED use leaderboard.deleteAllEntries(identifier, deleteRunningTotals)
 or leaderboard.deleteEntriesForCustomId(identifier, deleteRunningTotals, customIdFilter).</b>
Deletes the entry from the leaderboard that correspond to this identifier.
This method is not supported for leaderboards with custom IDs and will throw an java.lang.UnsupportedOperationException
This method only works for realtime leaderboards
If deleteRunningTotals is true, all running total data for these entries will also be deleted
deleting running totals may affect other leaderbaords using the same running totals
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.deleteEntry(myPlayerId, true);</pre>
## getPropertySet
_signature_ getPropertySet()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts
Returns the property set associated with this leaderboard
## getRankForScore
_signature_ getRankForScore(JSON score)</p>
_returns_ number</p>

Returns the rank a given score would be at on this Global leaderboard, without it actually being entered into the leaderboard.
Calling this on a Team or Social leaderboard will return null.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var rank = leaderboard.getRankForScore({"score" : 123});</pre>
## rebuildLeaderboard
_signature_ rebuildLeaderboard(boolean awardAchievements)</p>
_returns_ void</p>

Drops the current leaderboard and it rebuilds it from the running totals.
The current leaderboard may not have valid ranks for the duration of this process.
You can only rebuild realtime leaderboards. You cannot rebuild partitioned leaderboards, you can only rebuild the individual partitions.
If the flag awardAchievements is set to true, at the end of the rebuild process the appropriate achievements will be awarded
Please use with care, because during the rebuild process any new data coming from the players might temporarily have incorrect ranks
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">leaderboard.rebuildLeaderboard(true);</pre>
