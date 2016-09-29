# SparkLeaderboardOperations

A comparison operation on the owners (players in a player-based leaderboard, teams in a team-based leaderboard) of entries within leaderboards.

<pre rel="highlighter" code-brush="js" contenteditable="false">var operation = Spark.getLeaderboards().union(lb1, lb2);</pre>


## union
_signature_ union([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs a union on the set of owners returned as result of evaluating this operation and the owners of entries within the given leaderboard.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = operation.union(rhs).evaluate();</pre>


_signature_ union([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs a union on the set of owners returned as result of evaluating this operation and the set of owners returned as result of evaluating the given operation.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var inAny = operation.union(rhs).evaluate();</pre>

## intersection
_signature_ intersection([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs an intersection on the set of owners returned as result of evaluating this operation and the owners of entries within the given leaderboard.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = operation.intersection(rhs).evaluate();</pre>


_signature_ intersection([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs an intersection on the set of owners returned as result of evaluating this operation and the set of owners returned as result of evaluating the given operation.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var inBoth = operation.intersection(rhs).evaluate();</pre>

## difference
_signature_ difference([SparkLeaderboard](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboard.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs a difference on the set of owners returned as result of evaluating this operation and the owners of entries within the given leaderboard.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = operation.difference(rhs).evaluate();</pre>


_signature_ difference([SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md) rhs)</p>
_returns_ [SparkLeaderboardOperations](/API Documentation/Cloud Code API/Leaderboards/SparkLeaderboardOperations.md)</p>

<b>validity</b> All Scripts

Performs a difference on the set of owners returned as result of evaluating this operation and the set of owners returned as result of evaluating the given operation.

Returns a new SparkLeaderboardOperations object to allow further operations to be chained before evaluation.

To obtain the result of the operation call evaluate() on the SparkLeaderboardOperations returned.

<b>params</b>

rhs - the the right-hand side of the operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var onlyInFirst = operation.difference(rhs).evaluate();</pre>

## evaluate
_signature_ evaluate()</p>
_returns_ string[]</p>

<b>validity</b> All Scripts

Returns an array of ids representing the result set of evaluating this operation.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var results = operation.evaluate();</pre>

