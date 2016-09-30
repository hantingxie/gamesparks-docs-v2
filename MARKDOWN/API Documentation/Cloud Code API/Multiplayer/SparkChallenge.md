---
src: /API Documentation/Cloud Code API/Multiplayer/SparkChallenge.md
---

# SparkChallenge

Provides access to a challenge's details.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var challenge = Spark.getChallenge(mychallengeid);</pre>


## getRunState
_signature_ getRunState()</p>
_returns_ string</p>

The run state of the object. Valid states are:

ACCEPTED - All players have accepted the challenge

WAITING - The challenge is in it's waiting state, between expiryDate and startDate

RUNNING - The challenge is running

COMPLETE - The challenge is complete

DECLINED - All players have declined the challenge

EXPIRED - The expiry time for the challenge has passed before all players have accepted

ISSUED - The challenge has been issued but is waiting for other to accept before play can begin

WITHDRAWN - The challenger has withdrawn the challenge

LAPSED - The end time of this challenge has passed before the challenge was started

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var runState = Spark.getChallenge(mychallengeid).getRunState();</pre>

## getId
_signature_ getId()</p>
_returns_ string</p>

Gets the ID of this challenge.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var id = Spark.getChallenge(mychallengeid).getId();</pre>

## getShortCode
_signature_ getShortCode()</p>
_returns_ string</p>

Returns the shortCode of the challenge

Can be useful when block or code should only run for a particular challenge type.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var shortCode = Spark.getChallenge(mychallengeid).getShortCode();</pre>

## winChallenge
_signature_ winChallenge([SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md) winner)</p>
_returns_ void</p>

Complete the challenge and uses the provided SparkPlayer as the winner.

If the supplied SparkPlayer is not part of the challenge this call will be ignored (silently)

<b>params</b>

winner - the SparkPlayer to set as the winner

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getChallenge(mychallengeid).winChallenge(aPlayer);</pre>

## drawChallenge
_signature_ drawChallenge()</p>
_returns_ void</p>

Complete the challenge with no winner.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getChallenge(mychallengeid).drawChallenge();</pre>

## startChallenge
_signature_ startChallenge()</p>
_returns_ void</p>

Starts the challenge in the current state. This method only checks that the state is ISSUED or WAITING and that there is at least 2 players in the challenge 

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getChallenge(mychallengeid).startChallenge();</pre>

## getChallengedPlayerIds
_signature_ getChallengedPlayerIds()</p>
_returns_ string[]</p>

Returns a list of Players ID's that can be used to load the player details using Spark.getPlayer(String player)

<b>returns</b>

The array of player Ids this challenge was issued to

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var players = Spark.getChallenge(mychallengeid).getChallengedPlayerIds();</pre>

## getAcceptedPlayerIds
_signature_ getAcceptedPlayerIds()</p>
_returns_ string[]</p>

Returns a list of Players ID's that can be used to load the player details using Spark.getPlayer(String player)

<b>returns</b>

The array of player Ids who have accepted this challenge

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var players = Spark.getChallenge(mychallengeid).getAcceptedPlayerIds();</pre>

## getDeclinedPlayerIds
_signature_ getDeclinedPlayerIds()</p>
_returns_ string[]</p>

Returns a list of Players ID's that can be used to load the player details using Spark.getPlayer(String player)

<b>returns</b>

The array of player Ids who have declined this challenge

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var players = Spark.getChallenge(mychallengeid).getDeclinedPlayerIds()</pre>

## getChallengerId
_signature_ getChallengerId()</p>
_returns_ string</p>

Gets the player id of whoever issued the challenge.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var challengerId = Spark.getChallenge(mychallengeid).getChallengerId();</pre>

## consumeTurn
_signature_ consumeTurn(string playerId)</p>
_returns_ boolean</p>

<b>params</b>

Takes a turn for a player in a turn based challenge.

<b>params</b>

playerId - the id of the player who has taken their turn

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var challenge = Spark.getChallenge(mychallengeid).consumeTurn(playerId);</pre>

## removePlayer
_signature_ removePlayer(string playerId)</p>
_returns_ boolean</p>

<b>params</b>

Removes a player from this challenge.

<b>params</b>

playerId - the id of the player to remove

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var challenge = Spark.getChallenge(mychallengeid).removePlayer(playerId);</pre>

## getPrivateData
_signature_ getPrivateData(string name)</p>
_returns_ JSON</p>

Gets the value from a name value pair structure that allows custom data to be attached to this object. This data can either be complex JSON or simple values.

<b>params</b>

name - The name in the name value pair

<b>returns</b>

a JSON object

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getPrivateData("name");</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getChallenge().getPrivateData("name");</pre>

## setPrivateData
_signature_ setPrivateData(string name, JSON value)</p>
_returns_ void</p>

Allows arbitrary data to be added to the object being acted upon.

Sets a value into a name value pair structure that allows custom data to be attached to this object. This data can either be complex JSON or simple values.

The data is not visible to the client

<b>params</b>

name - The name in the name value pair

value - The value to set in the name value pair

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().setPrivateData("name", "value");</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getChallenge().setPrivateData("name", "value");</pre>

## removePrivateData
_signature_ removePrivateData(string name)</p>
_returns_ void</p>

Removes a value from a name value pair structure that allows custom data to be attached to this. This data can either be complex JSON or simple values.

<b>params</b>

name - The name in the name value pair

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().removePrivateData("name");</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getChallenge().removePrivateData("name");</pre>

## getScriptData
_signature_ getScriptData(string name)</p>
_returns_ JSON</p>

Gets the value from a name value pair structure that allows custom data to be attached to the challenge. This data can either be complex JSON or simple values.

<b>params</b>

name - The name in the name value pair

<b>returns</b>

a JSON object

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getScriptData("name");</pre>

## setScriptData
_signature_ setScriptData(string name, JSON value)</p>
_returns_ void</p>

Allows arbitrary data to be added to the object being acted upon.

Sets a value into a name value pair structure that allows custom data to be attached to the challenge. This data can either be complex JSON or simple values.

The data is visible to the client

This data is sent to the player(s) in the 'scriptData' attribute of the Request, Response or Message object.

When scriptData is set to a request, it gets set against the response that will be returned to the player. This allows basic communication between request and response scripts.

<b>params</b>

name - The name in the name value pair

value - The value to set in the name value pair

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().setScriptData("name", "value");</pre>

## removeScriptData
_signature_ removeScriptData(string name)</p>
_returns_ void</p>

Removes a value from a name value pair structure that allows custom data to be attached to the challenge. This data can either be complex JSON or simple values.

<b>params</b>

name - The name in the name value pair

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().removeScriptData("name");</pre>

