# SparkPlayer

Provides access to a player details
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var player = Spark.getPlayer();</pre>
or
<pre rel="highlighter" code-brush="js" contenteditable="false">var player = Spark.loadPlayer(myplayerid);</pre>

## getDisplayName
_signature_ getDisplayName()</p>
_returns_ string</p>

Gets the display name of the player.
This may be null for a player who has only used device authentication. Other authentication mechanisms will return a value.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getDisplayName();</pre>
## persist
_signature_ persist()</p>
_returns_ void</p>

Saves the players data to the DB. By default, changes are persisted after the script executes. This method ensures changes are saved immediately so other scripts running in parallel see the chnges immediately.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().persist();</pre>
## getUserName
_signature_ getUserName()</p>
_returns_ string</p>

Gets the username name of the player.
For a player who has only used device authentication this value will be generated from the device id.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getDisplayName();</pre>
## getPlayerId
_signature_ getPlayerId()</p>
_returns_ string</p>

Gets the GameSparks ID of the player
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getPlayerId();</pre>
## credit1
_signature_ credit1(number quantity)</p>
_returns_ void</p>

Credits the currency1 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit1(20);</pre>

_signature_ credit1(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency1 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit1(20, "Loyalty Bonus");</pre>
## debit1
_signature_ debit1(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency1 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>returns</b>
 true if the debit was successful, false if the current balance was not sufficient
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit1(5, "Loser Penalty");</pre>

_signature_ debit1(number quantity)</p>
_returns_ boolean</p>

Debits the currency1 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to debit
<b>returns</b>
 true if the debit was successful, false if the current balance was not sufficient
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit1(5);</pre>
## credit2
_signature_ credit2(number quantity)</p>
_returns_ void</p>

Credits the currency2 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit2(20);</pre>

_signature_ credit2(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency2 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit2(20, "Loyalty Bonus");</pre>
## debit2
_signature_ debit2(number quantity)</p>
_returns_ boolean</p>

Debits the currency2 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit2(5);</pre>

_signature_ debit2(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency2 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit2(5, "Loser Penalty");</pre>
## credit3
_signature_ credit3(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency3 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit3(20, "Loyalty Bonus");</pre>

_signature_ credit3(number quantity)</p>
_returns_ void</p>

Credits the currency3 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit3(20);</pre>
## debit3
_signature_ debit3(number quantity)</p>
_returns_ boolean</p>

Debits the currency3 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit3(5);</pre>

_signature_ debit3(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency3 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit3(5, "Loser Penalty");</pre>
## credit4
_signature_ credit4(number quantity)</p>
_returns_ void</p>

Credits the currency4 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit4(20);</pre>

_signature_ credit4(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency4 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit4(20, "Loyalty Bonus");</pre>
## credit5
_signature_ credit5(number quantity)</p>
_returns_ void</p>

Credits the currency5 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit5(20);</pre>

_signature_ credit5(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency5 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit5(20, "Loyalty Bonus");</pre>
## credit6
_signature_ credit6(number quantity)</p>
_returns_ void</p>

Credits the currency6 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit6(20);</pre>

_signature_ credit6(number quantity, string reason)</p>
_returns_ void</p>

Credits the currency6 balance of the player with the amount specified.
<b>params</b>
quantity - the amount to credit
reason - the reason for the credit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().credit6(20, "Loyalty Bonus");</pre>
## debit4
_signature_ debit4(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency4 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit4(5, "Loser Penalty");</pre>

_signature_ debit4(number quantity)</p>
_returns_ boolean</p>

Debits the currency4 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit4(5);</pre>
## debit5
_signature_ debit5(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency5 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit5(5, "Loser Penalty");</pre>

_signature_ debit5(number quantity)</p>
_returns_ boolean</p>

Debits the currency5 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit5(5);</pre>
## debit6
_signature_ debit6(number quantity)</p>
_returns_ boolean</p>

Debits the currency6 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit6(5);</pre>

_signature_ debit6(number quantity, string reason)</p>
_returns_ boolean</p>

Debits the currency6 balance of the player with the amount specified.
Returns true if the debit was successful, false if the current balance was not sufficient.
<b>params</b>
quantity - the amount to debit
reason - the reason for the debit
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().debit6(5, "Loser Penalty");</pre>
## getBalance1
_signature_ getBalance1()</p>
_returns_ number</p>

Gets the currency1 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance1();</pre>
## getBalance2
_signature_ getBalance2()</p>
_returns_ number</p>

Gets the currency2 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance2();</pre>
## getBalance3
_signature_ getBalance3()</p>
_returns_ number</p>

Gets the currency3 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance3();</pre>
## getBalance4
_signature_ getBalance4()</p>
_returns_ number</p>

Gets the currency4 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance4();</pre>
## getBalance5
_signature_ getBalance5()</p>
_returns_ number</p>

Gets the currency5 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance5();</pre>
## getBalance6
_signature_ getBalance6()</p>
_returns_ number</p>

Gets the currency6 balance of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var bal = Spark.getPlayer().getBalance6();</pre>
## addVGood
_signature_ addVGood(string shortCode, number quantity)</p>
_returns_ boolean</p>

Finds a virtual good by short code and adds the quantity specified to the player this SparkPlayer object represents.
Returns true if the add was successful. false if the shortcode does not exist, or the user already has the maximum amount of the specified good.
<b>params</b>
shortCode - the virtual good's short code
quantity - the amount to add
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().addVGood(vgShortCode, 42);</pre>

_signature_ addVGood(string shortCode, number quantity, string reason)</p>
_returns_ boolean</p>

Finds a virtual good by short code and adds the quantity specified to the player this SparkPlayer object represents.
Returns true if the add was successful. false if the shortcode does not exist, or the user already has the maximum amount of the specified good.
<b>params</b>
shortCode - the virtual good's short code
quantity - the amount to add
reason - the reason for adding the virtual good
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().addVGood(vgShortCode, 42, "Loyalty bonus");</pre>
## useVGood
_signature_ useVGood(string shortCode, number quantity, string reason)</p>
_returns_ boolean</p>

Removes a quantity of virtual goods from the player.
Returns true if the player had enough of the virtual good specified by short code. If the method returns false, no modification is made.
<b>params</b>
shortCode - the virtual good's short code
quantity - the amount to consume
reason - the reason for using the virtual good
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().useVGood(vgShortCode, 34, "Loser penalty");</pre>

_signature_ useVGood(string shortCode, number quantity)</p>
_returns_ boolean</p>

Removes a quantity of virtual goods from the player.
Returns true if the player had enough of the virtual good specified by short code. If the method returns false, no modification is made.
<b>params</b>
shortCode - the virtual good's short code
quantity - the amount to consume
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().useVGood(vgShortCode, 34);</pre>
## hasVGood
_signature_ hasVGood(string shortCode)</p>
_returns_ number</p>

Determines whether the player has a particular virtual good.
Returns the quantity of the virtual good the player has.
<b>params</b>
shortCode - the virtual good's short code
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().hasVGood(vgShortCode);</pre>
## addAchievement
_signature_ addAchievement(string shortCode)</p>
_returns_ boolean</p>

Adds an achievement to the player this SparkPlayer object represents.
The player will be given any award that is configured against the award in the developer portal.
Returns true if the achievement was added. false if the player already had the achievement, or the shortCode does not exist
<b>params</b>
shortCode - The shortCode of the achievement
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().addAchievement(shortCode);</pre>
## removeAchievement
_signature_ removeAchievement(string shortCode)</p>
_returns_ boolean</p>

Removes an achievement from the player.
Returns true if the achievement was removed. false if player did not have the achievement.
Returns false if the player did not have the achievement.
<b>params</b>
shortCode the shortCode of the achievement to remove
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().removeAchievement(shortCode);</pre>
## hasAchievement
_signature_ hasAchievement(string shortCode)</p>
_returns_ boolean</p>

Determines whether the player has a particular achievement.
Returns true if the player has the achievement
<b>params</b>
shortCode - The shortCode of the achievement
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().hasAchievement(shortCode);</pre>
## dismissMessage
_signature_ dismissMessage(string messageId)</p>
_returns_ boolean</p>

Allows a script to dismiss a given message that belongs to a player.
Returns true if a message was dismissed.
<b>params</b>
messageId
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().dismissMessage(messageId);</pre>
## getExternalIds
_signature_ getExternalIds()</p>
_returns_ JSON</p>

Returns a map of external system ids to external ids.
This allows you to determine, for example, the player facebook id.
Map keys: 'FB' - Indicates the ID is a facebook id
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().getExternalIds();</pre>
## getFriendIds
_signature_ getFriendIds()</p>
_returns_ JSON</p>

Returns an array of the player's social friend ids.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var friends = Spark.getPlayer().getFriendIds();</pre>
## isOnline
_signature_ isOnline()</p>
_returns_ boolean</p>

Returns true if this player is currently has an open WebSocket.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var online = Spark.getPlayer().isOnline();</pre>
## validatePassword
_signature_ validatePassword(string password)</p>
_returns_ boolean</p>

Validates the given password against the one stored for this player.
<b>params</b>
password - the password to validate
<b>returns</b>
true if the given password matches the one stored for this player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var doesPasswordMatch = Spark.getPlayer().validatePassword(passwordEnteredByPlayer);</pre>
## setPassword
_signature_ setPassword(string password)</p>
_returns_ void</p>

Sets a new password for this player.
<b>params</b>
password - the password to set
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().setPassword(password);</pre>
## isHiddenOnLeaderboards
_signature_ isHiddenOnLeaderboards()</p>
_returns_ boolean</p>

Boolean value indicating if this player is currently being hidden from leaderboards.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var hidden = Spark.getPlayer().isHidden();</pre>
## hideOnLeaderboards
_signature_ hideOnLeaderboards()</p>
_returns_ void</p>

Hide the player from current leaderboards.  Prevents any new scores posted showing up as well.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().hideOnLeaderboards();</pre>
## showOnLeaderboards
_signature_ showOnLeaderboards()</p>
_returns_ void</p>

Show the player on current leaderboards, redisplaying any existing scores.  New scores will begin to show up on leaderboards again as they are recorded.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.getPlayer().showOnLeaderboards();</pre>
## getPushRegistrations
_signature_ getPushRegistrations()</p>
_returns_ [SparkPushRegistration](/API Documentation/Cloud Code API/Player/SparkPushRegistration.md)[]</p>

Gets push registrations of the player
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().getPushRegistrations();</pre>
## removePushRegistration
_signature_ removePushRegistration(string id)</p>
_returns_ void</p>

Removes the registration with the given id.  The device associated with this registration will no longer receive push notifications for this player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().removePushRegistration(registrationId);</pre>
## setSegmentValue
_signature_ setSegmentValue(string segmentType, string segmentValue)</p>
_returns_ void</p>

Sets a value for a single segment against the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().setSegmentValue("PROFILE", "P1");</pre>
## getSegmentValue
_signature_ getSegmentValue(string segmentType)</p>
_returns_ string</p>

Gets a value for a single segment from the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var profileSegmentValue = Spark.getPlayer().getSegmentValue("PROFILE");</pre>
## getSegments
_signature_ getSegments()</p>
_returns_ JSON</p>

Gets all segment values from the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var segmentValue = Spark.getPlayer().getSegmentValues();</pre>
## disconnect
_signature_ disconnect(boolean excludeCurrent)</p>
_returns_ void</p>

Disconnects this player, a SessionTerminatedMessage will be sent to the socket, and the socket will be unauthenticated
<b>params</b>
excludeCurrent - If the script is running in the context of the user being disconnected, the current socket will not be disconnected
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().disconnect(true);</pre>
## getAchievements
_signature_ getAchievements()</p>
_returns_ string[]</p>

Gets all achievements from this player
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().getAchievements();</pre>
## getVirtualGoods
_signature_ getVirtualGoods()</p>
_returns_ JSON</p>

Gets all virtual goods from the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var goods = Spark.getPlayer().getVirtualGoods();</pre>
## resetAuthTokens
_signature_ resetAuthTokens()</p>
_returns_ void</p>

Removes all auth tokens for this user, this will force a re-authentication.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().resetAuthTokens();</pre>

_signature_ resetAuthTokens(boolean excludeCurrent)</p>
_returns_ void</p>

Removes auth tokens for this user, this will force a re-authentication.
<b>params</b>
excludeCurrent - If the script is running in the context of the user having tokens reset, the current token will not be reset
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().resetAuthTokens(true);</pre>
## getLastSeen
_signature_ getLastSeen()</p>
_returns_ date</p>

Gets the lastSeen value for the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var lastSeen = Spark.getPlayer().getLastSeen();</pre>
## unlock
_signature_ unlock()</p>
_returns_ void</p>

Unlocks the account for this player if it has been locked by too many failed login attempts.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().unlock();</pre>
## getCreationDate
_signature_ getCreationDate()</p>
_returns_ date</p>

Gets the creation date of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().getCreationDate();</pre>
## matchesMongoQuery
_signature_ matchesMongoQuery(ScriptableObject mongoQuery)</p>
_returns_ boolean</p>

Gets the creation date of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().getCreationDate();</pre>
## matchesMongoQueryString
_signature_ matchesMongoQueryString(string mongoQueryString)</p>
_returns_ boolean</p>

Checks if this player would be returned by the given mongo query (as a string).
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().matchesMongoQueryString("");</pre>
## getExperimentSegments
_signature_ getExperimentSegments()</p>
_returns_ [SparkPlayerExperimentSegment](/API Documentation/Cloud Code API/Player/SparkPlayerExperimentSegment.md)[]</p>

Returns the current experiment segments of the player.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().getExperimentSegments();</pre>
## removeExperiment
_signature_ removeExperiment(number experimentId)</p>
_returns_ boolean</p>

Removes the player from the given experiment.
<b>returns</b>
 true if the player was part of the experiment, false if the player was not part of the experiment
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().removeExperiment();</pre>
## setExperimentSegment
_signature_ setExperimentSegment(number experimentId, string experimentSegmentName)</p>
_returns_ boolean</p>

Sets the experiment segment for the player.
<b>returns</b>
 true if the experiment segment was added to the player, false if the player already had the experiment segment
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getPlayer().setExperimentSegment(47, "FireSale");</pre>
## deletePlayer
_signature_ deletePlayer()</p>
_returns_ void</p>

Deletes this player and associated data from system collections.
Note that any data linked to the player in runtime collections is not deleted, since the GameSparks platform has no way of identifying this data automatically.
This deletion is irreversible and should be used with extreme caution.
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">var userName = Spark.loadPlayer("57f4af757d196627bc79abc9").deletePlayer();</pre>
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
