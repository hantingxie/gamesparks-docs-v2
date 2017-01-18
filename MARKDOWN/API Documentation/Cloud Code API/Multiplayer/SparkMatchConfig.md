# SparkMatchConfig

Contains configuration information for the match


## getShortCode

_signature_ getShortCode()</p>
_returns_ string</p>

<b>validity</b> All Scripts
Returns the shortCode of the match

## getName

_signature_ getName()</p>
_returns_ string</p>

<b>validity</b> All Scripts
Returns the name of the match

## getDescription

_signature_ getDescription()</p>
_returns_ string</p>

<b>validity</b> All Scripts
Returns the description of the match

## getMinPlayers

_signature_ getMinPlayers()</p>
_returns_ number</p>

<b>validity</b> All Scripts
Returns the minimum number of players in the match

## getMaxPlayers

_signature_ getMaxPlayers()</p>
_returns_ number</p>

<b>validity</b> All Scripts
Returns the minimum number of players in the match

## getRealtime

_signature_ getRealtime()</p>
_returns_ boolean</p>

<b>validity</b> All Scripts
Returns the minimum number of players in the match

## getRealtimeScript

_signature_ getRealtimeScript()</p>
_returns_ string</p>

<b>validity</b> All Scripts
Returns the Realtime script

## getDropInDropOut

_signature_ getDropInDropOut()</p>
_returns_ boolean</p>

<b>validity</b> All Scripts
Returns true if the match is Drop In/Drop Out

## getDropInDropOutExpire

_signature_ getDropInDropOutExpire()</p>
_returns_ number</p>

<b>validity</b> All Scripts
Returns the number of seconds before Drop In/Drop Out expires

## getManuallyMatch

_signature_ getManuallyMatch()</p>
_returns_ boolean</p>

<b>validity</b> All Scripts
Returns true if the match is a manual match

## getPlayerDisconnectThreshold

_signature_ getPlayerDisconnectThreshold()</p>
_returns_ number</p>

<b>validity</b> All Scripts
Returns the number of seconds before players are disconnected for Drop In/Drop Out matches

## getThresholds

_signature_ getThresholds()</p>
_returns_ List</p>

<b>validity</b> All Scripts
Returns a list of thresholds in the match

## createPendingMatch

_signature_ createPendingMatch(string matchGroup, number skill, [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>
_returns_ [PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md)</p>

<b>validity</b> All Scripts
Creates a new pending match containing the given players.
Any existing pending matches for these players with the same matchGroup will be cancelled.

## createPendingMatchWithCustomQuery

_signature_ createPendingMatchWithCustomQuery(string matchGroup, number skill, JSON customQuery, JSON matchData, [SparkPlayer](/API Documentation/Cloud Code API/Player/SparkPlayer.md)[] players)</p>
_returns_ [PendingMatch](/API Documentation/Cloud Code API/Multiplayer/PendingMatch.md)</p>

<b>validity</b> All Scripts
Creates a new pending match containing the given players.
Any existing pending matches for these players with the same matchGroup will be cancelled.
