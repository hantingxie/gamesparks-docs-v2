---
src: /API Documentation/Cloud Code API/Multiplayer/PendingMatch.md
---

# PendingMatch

An object that represents a pending match.

## getId
_signature_ getId()</p>
_returns_ string</p>

<b>validity</b> All Scripts
The ID for the pending match.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.getId();</pre>
## getMatchShortCode
_signature_ getMatchShortCode()</p>
_returns_ string</p>

<b>validity</b> All Scripts
The match shortCode for the pending match.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.getMatchShortCode();</pre>
## getMatchGroup
_signature_ getMatchGroup()</p>
_returns_ string</p>

<b>validity</b> All Scripts
The match group for the pending match.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.getMatchGroup();</pre>
## getSkill
_signature_ getSkill()</p>
_returns_ number</p>

<b>validity</b> All Scripts
The average skill of players in this pending match.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.getSkill();</pre>
## getMatchedPlayers
_signature_ getMatchedPlayers()</p>
_returns_ SparkMatchedPlayer[]</p>

<b>validity</b> All Scripts
The players already part of this pending match.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.getMatchedPlayers();</pre>
## joinPendingMatch
_signature_ joinPendingMatch([PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md) pendingMatchToJoin)</p>
_returns_ [PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md)</p>

<b>validity</b> All Scripts
Join this pending match to the given pending match.
<b>returns</b>
The merged SparkPendingMatch if it was joined successfully,
or null if the pendingMatch could not be joined.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.joinPendingMatch(otherPendingMatch);</pre>
## findPendingMatches
_signature_ findPendingMatches(number maxMatchesToFind)</p>
_returns_ SparkPendingMatch[]</p>

<b>validity</b> All Scripts
Find pending matches that are suitable for matchmaking with this one.
<b>parameters</b>
maxMatchesToFind - the maximum number of results to return
<b>returns</b>
An array of pending matches suitable for matching with this one.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">pendingMatch.findPendingMatches();</pre>
