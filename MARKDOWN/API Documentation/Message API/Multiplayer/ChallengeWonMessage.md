
# ChallengeWonMessage


A message indicating that the challenge has been won.

This message is only sent to the individual player who has won the challenge


<a href="https://api.gamesparks.net/#challengewonmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challenge | No | Challenge | An object representing the challenge.
currency1Won | No | number | The amount of type 1 currency the player has won.
currency2Won | No | number | The amount of type 2 currency the player has won.
currency3Won | No | number | The amount of type 3 currency the player has won.
currency4Won | No | number | The amount of type 4 currency the player has won.
currency5Won | No | number | The amount of type 5 currency the player has won.
currency6Won | No | number | The amount of type 6 currency the player has won.
leaderboardData | No | LeaderboardData | The leaderboard data associated with this challenge.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.
winnerName | No | string | The winning player's name.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### PlayerTurnCount

Represents the number of turns a player has taken in a turn based challenge.

Parameter | Type | Description
--------- | ---- | -----------
count | string | The number of turns that the player has taken so far during this challenge.
playerId | string | The unique player id.

### Challenge

A nested object that represents the challenge data.

Parameter | Type | Description
--------- | ---- | -----------
accepted | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that have accepted this challenge.
challengeId | string | A unique identifier for this challenge.
challengeMessage | string | The message included in the challenge by the challenging player who created the challenge.
challengeName | string | The name of the challenge that this message relates to.
challenged | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that were challenged in this challenge.
challenger | [PlayerDetail](#playerdetail) | Details of the player who issued this challenge.
currency1Wager | number | The amount of type 1 currency that has been wagered on this challenge.
currency2Wager | number | The amount of type 2 currency that has been wagered on this challenge.
currency3Wager | number | The amount of type 3 currency that has been wagered on this challenge.
currency4Wager | number | The amount of type 4 currency that has been wagered on this challenge.
currency5Wager | number | The amount of type 5 currency that has been wagered on this challenge.
currency6Wager | number | The amount of type 6 currency that has been wagered on this challenge.
declined | [PlayerDetail[]](#playerdetail) | A list of PlayerDetail objects that represents the players that have declined this challenge.
endDate | date | The date when the challenge ends.
expiryDate | date | The latest date that a player can accept the challenge.
maxTurns | number | The maximum number of turns that this challenge is configured for.
nextPlayer | string | In a turn based challenge this fields contains the player's id whose turn it is next.
scriptData | ScriptData[] | ScriptData is arbitrary data that can be stored in a challenge instance by a Cloud Code script.
shortCode | string | The challenge's short code.
startDate | date | The date when the challenge starts.
state | string | One of these possible state values: ISSUED, EXPIRED, ACCEPTED, DECLINED, COMPLETE, WITHDRAWN, RUNNING, WAITING, RECEIVED
turnCount | [PlayerTurnCount[]](#playerturncount) | A collection containing the number of turns taken by each player that has accepted the challenge.

### PlayerDetail

An object representing a player's id and name

Parameter | Type | Description
--------- | ---- | -----------
externalIds | JSON | A player's external identifiers
id | string | A player's id
name | string | A player's name

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
	ChallengeWonMessage.Listener = (message) => {
	var challenge = message.Challenge; 
	long? currency1Won = message.Currency1Won; 
	long? currency2Won = message.Currency2Won; 
	long? currency3Won = message.Currency3Won; 
	long? currency4Won = message.Currency4Won; 
	long? currency5Won = message.Currency5Won; 
	long? currency6Won = message.Currency6Won; 
	var leaderboardData = message.LeaderboardData; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	string winnerName = message.WinnerName; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".ChallengeWonMessage",
		function (message:ChallengeWonMessage):void {
		var challenge:Challenge = message.getChallenge(); 
		var currency1Won:Number = message.getCurrency1Won(); 
		var currency2Won:Number = message.getCurrency2Won(); 
		var currency3Won:Number = message.getCurrency3Won(); 
		var currency4Won:Number = message.getCurrency4Won(); 
		var currency5Won:Number = message.getCurrency5Won(); 
		var currency6Won:Number = message.getCurrency6Won(); 
		var leaderboardData:LeaderboardData = message.getLeaderboardData(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		var winnerName:String = message.getWinnerName(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSChallengeWonMessage:^(GSChallengeWonMessage* message) {
	GSChallenge* challenge = [message getChallenge]; 
	NSNumber* currency1Won = [message getCurrency1Won]; 
	NSNumber* currency2Won = [message getCurrency2Won]; 
	NSNumber* currency3Won = [message getCurrency3Won]; 
	NSNumber* currency4Won = [message getCurrency4Won]; 
	NSNumber* currency5Won = [message getCurrency5Won]; 
	NSNumber* currency6Won = [message getCurrency6Won]; 
	GSLeaderboardData* leaderboardData = [message getLeaderboardData]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	NSString* winnerName = [message getWinnerName]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setChallengeWonMessageListener(
		new GSEventConsumer<ChallengeWonMessage>() {
			public void onEvent(ChallengeWonMessage event) {
		Challenge challenge = message.getChallenge(); 
		Long currency1Won = message.getCurrency1Won(); 
		Long currency2Won = message.getCurrency2Won(); 
		Long currency3Won = message.getCurrency3Won(); 
		Long currency4Won = message.getCurrency4Won(); 
		Long currency5Won = message.getCurrency5Won(); 
		Long currency6Won = message.getCurrency6Won(); 
		LeaderboardData leaderboardData = message.getLeaderboardData(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String title = message.getTitle(); 
		String winnerName = message.getWinnerName(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnChallengeWonMessage(GS& gsInstance, const ChallengeWonMessage& message)
	{
	Types::Challenge* challenge = message.getChallenge(); 
	Optional::t_LongOptional currency1Won = message.getCurrency1Won(); 
	Optional::t_LongOptional currency2Won = message.getCurrency2Won(); 
	Optional::t_LongOptional currency3Won = message.getCurrency3Won(); 
	Optional::t_LongOptional currency4Won = message.getCurrency4Won(); 
	Optional::t_LongOptional currency5Won = message.getCurrency5Won(); 
	Optional::t_LongOptional currency6Won = message.getCurrency6Won(); 
	Types::LeaderboardData* leaderboardData = message.getLeaderboardData(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	gsstl::string winnerName = message.getWinnerName(); 
	}
	...
	GS.SetMessageListener(OnChallengeWonMessage);
```

