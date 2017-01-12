# SparkLeaderboards

Provides access to the leaderboards for the current game.
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboards = Spark.getLeaderboards();</pre>

## getLeaderboard
_signature_ getLeaderboard(string shortCode)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a SparkLeaderboard object by its shortCode.
<b>params</b>
shortCode - the shortCode of the leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getLeaderboard(shortCode);</pre>
## getSocialLeaderboard
_signature_ getSocialLeaderboard(string shortCode, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode, where the social group contains the current player and the players with the given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
shortCode - the shortCode of the leaderboard.
friendsIds - the ids of the other players to be included in this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getSocialLeaderboard(shortCode, myplayerids);</pre>
## getInverseSocialLeaderboard
_signature_ getInverseSocialLeaderboard(string shortCode, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode for the current player, where the social group excludes the players with the given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
shortCode - the shortCode of the leaderboard.
friendsIds - the ids of the other players to be excluded from this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseSocialLeaderboard(shortCode, myplayerids);</pre>
## getSocialLeaderboardAs
_signature_ getSocialLeaderboardAs(string shortCode, string playerId, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode, where the social group contains the player with the given playerId and the players with given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
shortCode - the shortCode of the leaderboard.
playerId - the playerId to load the social leaderboard for.
friendsIds - the ids of the other players to be included in this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getSocialLeaderboardAs(shortCode, myplayerid, myplayerids);</pre>
## getInverseSocialLeaderboardAs
_signature_ getInverseSocialLeaderboardAs(string shortCode, string playerId, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode for the given player, where the social group excludes the players with the given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
shortCode - the shortCode of the leaderboard.
playerId - the playerId to load the social leaderboard for.
friendsIds - the ids of the other players to be excluded from this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseSocialLeaderboardAs(shortCode, myplayerid, myplayerids);</pre>
## getTeamLeaderboard
_signature_ getTeamLeaderboard(string shortCode, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode, where the social group contains the current player and the players belonging to the teams with the given teamIds
<b>params</b>
shortCode - the shortCode of the leaderboard.
teamids - the ids of the teams to be included in this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getTeamLeaderboard(shortCode, myteamids);</pre>
## getInverseTeamLeaderboard
_signature_ getInverseTeamLeaderboard(string shortCode, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode for the current player, where the social group excludes the players belonging to the teams with the given teamIds
<b>params</b>
shortCode - the shortCode of the leaderboard.
teamids - the ids of the teams to be excluded from this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseTeamLeaderboard(shortCode, myteamids);</pre>
## getTeamLeaderboardAs
_signature_ getTeamLeaderboardAs(string shortCode, string playerId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode, where the social group contains the player for the given playerId and the players belonging to the teams with the given teamIds
<b>params</b>
shortCode - the shortCode of the leaderboard.
playerId - the playerId to load the social leaderboard for.
teamids - the ids of the teams to be included in this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getTeamLeaderboard(shortCode, myplayerid, myteamids);</pre>
## getInverseTeamLeaderboardAs
_signature_ getInverseTeamLeaderboardAs(string shortCode, string playerId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard object by its shortCode for the given player, where the social group excludes the players belonging to the teams with the given teamIds
<b>params</b>
shortCode - the shortCode of the leaderboard.
playerId - the playerId to load the social leaderboard for.
teamids - the ids of the teams to be excluded from this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseTeamLeaderboard(shortCode, myplayerid, myteamids);</pre>
## listLeaderboards
_signature_ listLeaderboards()</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)[]</p>

<b>validity</b> All Scripts
Gives access to all leaderboards configured for the game
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboards = Spark.getLeaderboards().listLeaderboards();</pre>
## getChallengeLeaderboard
_signature_ getChallengeLeaderboard(string challengeInstanceId)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a SparkLeaderboard object for a specific challenge by the challengeInstanceId.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getChallengeLeaderboard(challengeInstanceId);</pre>
## getSocialChallengeLeaderboard
_signature_ getSocialChallengeLeaderboard(string challengeInstanceId, string[] friendsIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge, where the social group contains the current player and the given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
friendsIds - the ids of the other players to be included in this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getSocialChallengeLeaderboard(challengeInstanceId, myplayerids);</pre>
## union
_signature_ union([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a union on the set of owners of entries within the first leaderboard and the set of owners of entries within the second.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = Spark.getLeaderboards().union(lhs, rhs).evaluate();</pre>

_signature_ union([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a union on the set of owners returned as result of evaluating the operation and the owners of entries within the leaderboard.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = Spark.getLeaderboards().union(lhs, rhs).evaluate();</pre>

_signature_ union([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a union on the set of owners of entries within the leaderboard and the set of owners returned as result of evaluating the operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = Spark.getLeaderboards().union(lhs, rhs).evaluate();</pre>

_signature_ union([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a union on the set of owners returned as result of evaluating the first operation and the set of owners returned as result of evaluating the second operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = Spark.getLeaderboards().union(lhs, rhs).evaluate();</pre>
## getInverseSocialChallengeLeaderboard
_signature_ getInverseSocialChallengeLeaderboard(string challengeInstanceId, string[] friendsIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge for the current player, where the social group excludes the players with the given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
friendsIds - the ids of the other players to be excluded from this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseSocialChallengeLeaderboard(challengeInstanceId, myplayerids);</pre>
## getSocialChallengeLeaderboardAs
_signature_ getSocialChallengeLeaderboardAs(string challengeInstanceId, string playerId, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge, where the social group contains the player with the given playerId and the players with given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
playerId - the playerId to load the social leaderboard for.
friendsIds - the ids of the other players to be included in this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getSocialChallengeLeaderboardAs(challengeInstanceId, myplayerid, myplayerids);</pre>
## getInverseSocialChallengeLeaderboardAs
_signature_ getInverseSocialChallengeLeaderboardAs(string challengeInstanceId, string playerId, string[] friendIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge for the current player, where the social group excludes the players with given playerIds.
If no playerIds are provided the player's game friends are used.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
playerId - the playerId to load the social leaderboard for.
friendsIds - the ids of the players to be excluded from this social leaderboard.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseSocialChallengeLeaderboardAs(challengeInstanceId, myplayerid, myplayerids);</pre>
## getTeamChallengeLeaderboard
_signature_ getTeamChallengeLeaderboard(string challengeInstanceId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge, where the social group contains the current player and the players belonging to the teams with the given teamIds.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
teamids - the ids of the teams to be included in this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getTeamChallengeLeaderboard(challengeInstanceId, myteamids);</pre>
## getInverseTeamChallengeLeaderboard
_signature_ getInverseTeamChallengeLeaderboard(string challengeInstanceId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge for the current player, where the social group excludes the players belonging to the teams with the given teamIds.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
teamids - the ids of the teams to be excluded from this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseTeamChallengeLeaderboard(challengeInstanceId, myteamids);</pre>
## intersection
_signature_ intersection([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs an intersection on the set of owners returned as result of evaluating the operation and the owners of entries within the leaderboard.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = Spark.getLeaderboards().intersection(lhs, rhs).evaluate();</pre>

_signature_ intersection([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs an intersection on the set of owners of entries within the leaderboard and the set of owners returned as result of evaluating the operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = Spark.getLeaderboards().intersection(lhs, rhs).evaluate();</pre>

_signature_ intersection([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs an intersection on the set of owners returned as result of evaluating the first operation and the set of owners returned as result of evaluating the second operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = Spark.getLeaderboards().intersection(lhs, rhs).evaluate();</pre>

_signature_ intersection([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs an intersection on the set of owners of entries within the first leaderboard and the set of owners of entries within the second.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = Spark.getLeaderboards().intersection(lhs, rhs).evaluate();</pre>
## getTeamChallengeLeaderboardAs
_signature_ getTeamChallengeLeaderboardAs(string challengeInstanceId, string playerId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge where the social group contains the player for the given playerId and the players belonging to the teams with the given teamIds.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
playerId - the playerId to load the social leaderboard for.
teamids - the ids of the teams to be included in this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getTeamChallengeLeaderboard(challengeInstanceId, myplayerid, myteamids);</pre>
## getInverseTeamChallengeLeaderboardAs
_signature_ getInverseTeamChallengeLeaderboardAs(string challengeInstanceId, string playerId, string[] teamIds)</p>
_returns_ [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md)</p>

<b>validity</b> All Scripts
Allows a script to load a social SparkLeaderboard for a specific challenge for the given player, where the social group  excludes the players belonging to the teams with the given teamIds.
<b>params</b>
challengeInstanceId - the id of the challenge instance to load the leaderboard for.
playerId - the playerId to load the social leaderboard for.
teamids - the ids of the teams to be excluded from this social leaderboard
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var leaderboard = Spark.getLeaderboards().getInverseTeamChallengeLeaderboard(challengeInstanceId, myplayerid, myteamids);</pre>
## difference
_signature_ difference([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a difference on the set of owners of entries within the first leaderboard and the set of owners of entries within the second.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = Spark.getLeaderboards().difference(lhs, rhs).evaluate();</pre>

_signature_ difference([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a difference on the set of owners of entries within the leaderboard and the set of owners returned as result of evaluating the operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = Spark.getLeaderboards().difference(lhs, rhs).evaluate();</pre>

_signature_ difference([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a difference on the set of owners returned as result of evaluating the operation and the owners of entries within the leaderboard.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = Spark.getLeaderboards().difference(lhs, rhs).evaluate();</pre>

_signature_ difference([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) lhs, [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts
Performs a difference on the set of owners returned as result of evaluating the first operation and the set of owners returned as result of evaluating the second operation.
Returns a SparkLeaderboardOperations object to allow further operations to be chained before evaluation.
To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.
<b>params</b>
lhs - the left-hand side of the operation.
rhs - the the right-hand side of the operation.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = Spark.getLeaderboards().difference(lhs, rhs).evaluate();</pre>
