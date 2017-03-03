# SparkMultiplayer

Provides access to the platform's multiplayer capabilities.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var multiplayer = Spark.getMultiplayer();</pre>



## createMatch

_signature_ createMatch([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Create a match between the given players.

<b>params</b>

players - An array of players to include in the match

<b>returns</b>

The matchId if a match was successfully created, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = Spark.getMultiplayer().createMatch(player1, player2);</pre>


## createMatchById

_signature_ createMatchById(string[] playerIds)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Create a match between the players for the given playerIds.

<b>params</b>

playerIds - An array of playerIds to include in the match

<b>returns</b>

The matchId if a match was successfully created, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = Spark.getMultiplayer().createMatchById(playerId1, playerId2);</pre>


## createMatchWithMatchId

_signature_ createMatchWithMatchId(string matchId, [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Create a match between the given players, using the given matchId.

<b>params</b>

matchId - The matchId to use when creating this match

players - An array of players to include in the match

<b>returns</b>

The matchId if a match was successfully created, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = Spark.getMultiplayer().createMatchWithMatchId("myId", player1, player2);</pre>


## createMatchByIdWithMatchId

_signature_ createMatchByIdWithMatchId(string matchId, string[] playerIds)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Create a match between the players for the given playerIds, using the given matchId.

<b>params</b>

matchId - The matchId to use when creating this match

playerIds - An array of playerIds to include in the match

<b>returns</b>

The matchId if a match was successfully created, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = Spark.getMultiplayer().createMatchById("myId", playerId1, playerId2);</pre>


## loadMatch

_signature_ loadMatch(string matchId)</p>

_returns_ [SparkMatch](/API Documentation/Cloud Code API/Multiplayer/SparkMatch.md)</p>

<b>validity</b> All Scripts

Load the match with the given matchId

<b>params</b>

matchId - The id of the match to load

<b>returns</b>

The match if a match was found with the given id

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchId = Spark.getMultiplayer().loadMatch(matchId);</pre>


## getMatchConfig

_signature_ getMatchConfig(string shortCode)</p>

_returns_ [SparkMatchConfig](/API Documentation/Cloud Code API/Multiplayer/SparkMatchConfig.md)</p>

<b>validity</b> All Scripts

Load the match configuration for the given shortCode

<b>params</b>

shortCode - The shortCode of the match configuration to load

<b>returns</b>

The match configuration if a one was found with the given shortCode

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var matchConfig = Spark.getMultiplayer().getMatchConfig(shortCode);</pre>


## loadPendingMatchById

_signature_ loadPendingMatchById(string pendingMatchId)</p>

_returns_ [PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md)</p>

<b>validity</b> All Scripts

Load the pending match with the given pendingMatchId

<b>params</b>

pendingMatchId - The id of the pending match to load

<b>returns</b>

The pending match if one was found with the given id

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var pendingMatch = Spark.getMultiplayer().loadPendingMatchById(pendingMatchId);</pre>


## loadPendingMatchByPlayer

_signature_ loadPendingMatchByPlayer([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md) player, string shortCode, string matchGroup)</p>

_returns_ [PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md)</p>

<b>validity</b> All Scripts

Load the pending match containing the given player for the match shortCode and match group.

<b>params</b>

player - A player within the pending match

shortCode - The shortCode of the match configuration for the pending match

matchGroup - The matchGroup for the pending match

<b>returns</b>

The pending match if one was found with the given id

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var pendingMatch = Spark.getMultiplayer().loadPendingMatchByPlayer(player, matchShortCode, matchGroup);</pre>


## cancelMatchmaking

_signature_ cancelMatchmaking([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md) player, string shortCode, string matchGroup)</p>

_returns_ void</p>

<b>validity</b> All Scripts

Cancel matchmaking for the given player, match shortCode and match group.

<b>params</b>

player - A player within a pending match

shortCode - The shortCode of the match configuration for the pending match

matchGroup - The matchGroup for the pending match

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getMultiplayer().cancelMatchmaking(player, matchShortCode, matchGroup);</pre>


