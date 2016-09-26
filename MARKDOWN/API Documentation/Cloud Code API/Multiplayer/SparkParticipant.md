---
src: /API Documentation/Cloud Code API/Multiplayer/SparkParticipant.md
---

# SparkParticipant

Provides the details of a participant in a match

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var participant = Spark.getMultiplayer().loadMatch(matchId).getParticipants[0];</pre>



## getPlayer
_signature_ getPlayer()</p>
_returns_ [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)</p>
<b>validity</b> All Scripts<b>returns</b>The SparkPlayer this participant represents<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var player = participant.getPlayer()</pre>

## getPeerId
_signature_ getPeerId()</p>
_returns_ number</p>
<b>validity</b> All Scripts<b>returns</b>The peerId of this participant<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var peerId = participant.getPeerId()</pre>

## getAccessToken
_signature_ getAccessToken()</p>
_returns_ string</p>
<b>validity</b> All Scripts<b>returns</b>An accessToken for this participant to connect to the realtime server<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var accessToken = participant.getAccessToken()</pre>

