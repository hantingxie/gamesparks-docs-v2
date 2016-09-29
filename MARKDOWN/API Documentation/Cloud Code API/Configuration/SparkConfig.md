# SparkConfig

Contains configuration information for the game


## getStage
_signature_ getStage()</p>
_returns_ string</p>

<b>validity</b> All Scripts

Returns the stage (preview or live) the game is running on

## getApiKey
_signature_ getApiKey()</p>
_returns_ string</p>

<b>validity</b> All Scripts

Returns the apiKey of the game

## getVirtualGoods
_signature_ getVirtualGoods()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the Virtual Goods configured against the game

## getVirtualGood
_signature_ getVirtualGood(string shortCode)</p>
_returns_ [SparkVirtualGood](/API Documentation/Cloud Code API/Configuration/SparkVirtualGood.md)</p>

<b>validity</b> All Scripts

Returns the virtual good with the supplied short code

## getAchievements
_signature_ getAchievements()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the Achievements configured against the game

## getAchievement
_signature_ getAchievement(string shortCode)</p>
_returns_ [SparkAchievement](/API Documentation/Cloud Code API/Configuration/SparkAchievement.md)</p>

<b>validity</b> All Scripts

Returns the achievement with the supplied short code

## getSegments
_signature_ getSegments()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the Segments configured against the game

## getSegment
_signature_ getSegment(string shortCode)</p>
_returns_ [SparkSegmentType](/API Documentation/Cloud Code API/Configuration/SparkSegmentType.md)</p>

<b>validity</b> All Scripts

Returns the segment with the supplied short code

## getTeams
_signature_ getTeams()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the Teams configured against the game

## getTeam
_signature_ getTeam(string shortCode)</p>
_returns_ [SparkTeamType](/API Documentation/Cloud Code API/Configuration/SparkTeamType.md)</p>

<b>validity</b> All Scripts

Returns the team with the supplied short code

## getChallenges
_signature_ getChallenges()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the Challenges configured against the game

## getChallenge
_signature_ getChallenge(string shortCode)</p>
_returns_ [SparkChallengeType](/API Documentation/Cloud Code API/Configuration/SparkChallengeType.md)</p>

<b>validity</b> All Scripts

Returns the challenge with the supplied short code

## getDownloadable
_signature_ getDownloadable(string shortCode)</p>
_returns_ [SparkDownloadable](/API Documentation/Cloud Code API/Configuration/SparkDownloadable.md)</p>

<b>validity</b> All Scripts

Returns the downloadable with the supplied short code

## getDownloadables
_signature_ getDownloadables()</p>
_returns_ [SparkDownloadable](/API Documentation/Cloud Code API/Configuration/SparkDownloadable.md)[]</p>

<b>validity</b> All Scripts

Returns a list of all the downloadables configured for this game

## getMatchConfigs
_signature_ getMatchConfigs()</p>
_returns_ JSON</p>

<b>validity</b> All Scripts

Returns a list of the match configurations for the game

## getMatchConfig
_signature_ getMatchConfig(string shortCode)</p>
_returns_ [SparkMatchConfig](/API Documentation/Cloud Code API/Multiplayer/SparkMatchConfig.md)</p>

<b>validity</b> All Scripts

Returns the match configuration with the supplied short code

