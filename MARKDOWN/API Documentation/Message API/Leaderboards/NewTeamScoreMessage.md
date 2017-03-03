---
src: /API Documentation/Message API/Leaderboards/NewTeamScoreMessage.md
---

# NewTeamScoreMessage


A message indicating that the player's team has achieved a new high score in the game.


<a href="https://api.gamesparks.net/#newteamscoremessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
leaderboardData | No | LeaderboardData | The new leaderboard data associated with this message.
leaderboardName | No | string | The leaderboard's name.
leaderboardShortCode | No | string | The leaderboard shortcode.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
rankDetails | No | LeaderboardRankDetails | The ranking information for the new score.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### LeaderboardRankDetails

Ranking information.

Parameter | Type | Description
--------- | ---- | -----------
friendsPassed | [LeaderboardData[]](#leaderboarddata) | The leaderboard entries of the players friends that were beaten as part of this score submission.
globalCount | number | The number of entries in this leaderboard.
globalFrom | number | The Global Rank of the player in this leaderboard before the score was submitted.
globalFromPercent | number | The old global rank of the player as a percentage of the total number of scores in this leaderboard .
globalTo | number | The Global Rank of the player in this leaderboard after the score was submitted.
globalToPercent | number | The new global rank of the player as a percentage of the total number of scores in this leaderboard .
socialCount | number | The number of friend entries the player has in this leaderboard.
socialFrom | number | The Social Rank of the player in this leaderboard before the score was submitted.
socialFromPercent | number | The old social rank of the player as a percentage of the total number of friend scores in this leaderboard.
socialTo | number | The Social Rank of the player in this leaderboard after the score was submitted.
socialToPercent | number | The old global rank of the player as a percentage of the total number of friend scores in this leaderboard.
topNPassed | [LeaderboardData[]](#leaderboarddata) | The leaderboard entries of the global players that were beaten as part of this score submission. Requires Top N to be configured on the leaderboard

### LeaderboardData

Leaderboard entry data

As well as the parameters below there may be others depending on your game's configuration.

Parameter | Type | Description
--------- | ---- | -----------
city | string | The city where the player was located when they logged this leaderboard entry.
country | string | The country code where the player was located when they logged this leaderboard entry.
externalIds | JSON | The players rank.
rank | number | The players rank.
userId | string | The unique player id for this leaderboard entry.
userName | string | The players display name.
when | string | The date when this leaderboard entry was created.


## Code Samples

<h3>C#</h3>
```cs
	NewTeamScoreMessage.Listener = (message) => {
	var leaderboardData = message.LeaderboardData; 
	string leaderboardName = message.LeaderboardName; 
	string leaderboardShortCode = message.LeaderboardShortCode; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	var rankDetails = message.RankDetails; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".NewTeamScoreMessage",
		function (message:NewTeamScoreMessage):void {
		var leaderboardData:LeaderboardData = message.getLeaderboardData(); 
		var leaderboardName:String = message.getLeaderboardName(); 
		var leaderboardShortCode:String = message.getLeaderboardShortCode(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var rankDetails:LeaderboardRankDetails = message.getRankDetails(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSNewTeamScoreMessage:^(GSNewTeamScoreMessage* message) {
	GSLeaderboardData* leaderboardData = [message getLeaderboardData]; 
	NSString* leaderboardName = [message getLeaderboardName]; 
	NSString* leaderboardShortCode = [message getLeaderboardShortCode]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	GSLeaderboardRankDetails* rankDetails = [message getRankDetails]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setNewTeamScoreMessageListener(
		new GSEventConsumer<NewTeamScoreMessage>() {
			public void onEvent(NewTeamScoreMessage event) {
		LeaderboardData leaderboardData = message.getLeaderboardData(); 
		String leaderboardName = message.getLeaderboardName(); 
		String leaderboardShortCode = message.getLeaderboardShortCode(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		LeaderboardRankDetails rankDetails = message.getRankDetails(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String title = message.getTitle(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnNewTeamScoreMessage(GS& gsInstance, const NewTeamScoreMessage& message)
	{
	Types::LeaderboardData* leaderboardData = message.getLeaderboardData(); 
	gsstl::string leaderboardName = message.getLeaderboardName(); 
	gsstl::string leaderboardShortCode = message.getLeaderboardShortCode(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	Types::LeaderboardRankDetails* rankDetails = message.getRankDetails(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	}
	...
	GS.SetMessageListener(OnNewTeamScoreMessage);
```

