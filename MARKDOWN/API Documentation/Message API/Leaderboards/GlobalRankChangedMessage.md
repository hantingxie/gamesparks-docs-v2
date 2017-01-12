
# GlobalRankChangedMessage


This message is sent to players when their rank in a global leaderboard changes such that they are knocked out of the configured 'Top N'.


<a href="https://api.gamesparks.net/#globalrankchangedmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
gameId | No | number | The game id that this message relates to.
leaderboardName | No | string | The leaderboard's name.
leaderboardShortCode | No | string | The leaderboard shortcode.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
them | No | LeaderboardData | The score details of the player whose score the receiving player has passed.
title | No | string | A textual title for the message.
you | No | LeaderboardData | The score details of the receiving player.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

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
	GlobalRankChangedMessage.Listener = (message) => {
	long? gameId = message.GameId; 
	string leaderboardName = message.LeaderboardName; 
	string leaderboardShortCode = message.LeaderboardShortCode; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	var them = message.Them; 
	string title = message.Title; 
	var you = message.You; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".GlobalRankChangedMessage",
		function (message:GlobalRankChangedMessage):void {
		var gameId:Number = message.getGameId(); 
		var leaderboardName:String = message.getLeaderboardName(); 
		var leaderboardShortCode:String = message.getLeaderboardShortCode(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var them:LeaderboardData = message.getThem(); 
		var title:String = message.getTitle(); 
		var you:LeaderboardData = message.getYou(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSGlobalRankChangedMessage:^(GSGlobalRankChangedMessage* message) {
	NSNumber* gameId = [message getGameId]; 
	NSString* leaderboardName = [message getLeaderboardName]; 
	NSString* leaderboardShortCode = [message getLeaderboardShortCode]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	GSLeaderboardData* them = [message getThem]; 
	NSString* title = [message getTitle]; 
	GSLeaderboardData* you = [message getYou]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setGlobalRankChangedMessageListener(
		new GSEventConsumer<GlobalRankChangedMessage>() {
			public void onEvent(GlobalRankChangedMessage event) {
		Long gameId = message.getGameId(); 
		String leaderboardName = message.getLeaderboardName(); 
		String leaderboardShortCode = message.getLeaderboardShortCode(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		LeaderboardData them = message.getThem(); 
		String title = message.getTitle(); 
		LeaderboardData you = message.getYou(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnGlobalRankChangedMessage(GS& gsInstance, const GlobalRankChangedMessage& message)
	{
	Optional::t_LongOptional gameId = message.getGameId(); 
	gsstl::string leaderboardName = message.getLeaderboardName(); 
	gsstl::string leaderboardShortCode = message.getLeaderboardShortCode(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	Types::LeaderboardData* them = message.getThem(); 
	gsstl::string title = message.getTitle(); 
	Types::LeaderboardData* you = message.getYou(); 
	}
	...
	GS.SetMessageListener(OnGlobalRankChangedMessage);
```

