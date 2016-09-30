---
src: /API Documentation/Message API/Multiplayer/MatchUpdatedMessage.md
---

# MatchUpdatedMessage


A message indicating that there has been an update to a pending match request, but it is not yet complete


<a href="https://api.gamesparks.net/#matchupdatedmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
addedPlayers | No | string[] | The players that joined this match
matchData | No | JSON | MatchData is arbitrary data that can be stored in a Match instance by a Cloud Code script.
matchGroup | No | string | The group the player was assigned in the matchmaking request
matchId | No | string | The id for this match instance
matchShortCode | No | string | The shortCode of the match type this message for
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
participants | No | Participant[] | The participants in this match
removedPlayers | No | string[] | The players that left this match
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.

## Nested types

### Participant

A nested object that represents a participant in a match.

Parameter | Type | Description
--------- | ---- | -----------
achievements | string[] | The achievements of the Player
displayName | string | The display name of the Player
externalIds | JSON | The external Id's of the Player
id | string | The id of the Player
online | boolean | The online status of the Player
participantData | JSON | A JSON Map of any data that was associated to this user
peerId | number | The peerId of this participant within the match
scriptData | JSON | The script data of the Player
virtualGoods | string[] | The virtual goods of the Player

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.


## Code Samples

<h3>C#</h3>
```cs
	MatchUpdatedMessage.Listener = (message) => {
	IList<string> addedPlayers = message.AddedPlayers; 
	GSData matchData = message.MatchData; 
	string matchGroup = message.MatchGroup; 
	string matchId = message.MatchId; 
	string matchShortCode = message.MatchShortCode; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<var> participants = message.Participants; 
	IList<string> removedPlayers = message.RemovedPlayers; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".MatchUpdatedMessage",
		function (message:MatchUpdatedMessage):void {
		var addedPlayers:Vector.<String> = message.getAddedPlayers(); 
		var matchData:Object = message.getMatchData(); 
		var matchGroup:String = message.getMatchGroup(); 
		var matchId:String = message.getMatchId(); 
		var matchShortCode:String = message.getMatchShortCode(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var participants:Vector.<Participant> = message.getParticipants(); 
		var removedPlayers:Vector.<String> = message.getRemovedPlayers(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSMatchUpdatedMessage:^(GSMatchUpdatedMessage* message) {
	NSArray* addedPlayers = [message getAddedPlayers]; 
	NSDictionary* matchData = [message getMatchData]; 
	NSString* matchGroup = [message getMatchGroup]; 
	NSString* matchId = [message getMatchId]; 
	NSString* matchShortCode = [message getMatchShortCode]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* participants = [message getParticipants]; 
	NSArray* removedPlayers = [message getRemovedPlayers]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setMatchUpdatedMessageListener(
		new GSEventConsumer<MatchUpdatedMessage>() {
			public void onEvent(MatchUpdatedMessage event) {
		List<String> addedPlayers = message.getAddedPlayers(); 
		GSData matchData = message.getMatchData(); 
		String matchGroup = message.getMatchGroup(); 
		String matchId = message.getMatchId(); 
		String matchShortCode = message.getMatchShortCode(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<Participant> participants = message.getParticipants(); 
		List<String> removedPlayers = message.getRemovedPlayers(); 
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
	void OnMatchUpdatedMessage(GS& gsInstance, const MatchUpdatedMessage& message)
	{
	gsstl:vector<gsstl::string> addedPlayers = message.getAddedPlayers(); 
	GSData matchData = message.getMatchData(); 
	gsstl::string matchGroup = message.getMatchGroup(); 
	gsstl::string matchId = message.getMatchId(); 
	gsstl::string matchShortCode = message.getMatchShortCode(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<Types::Participant*> participants = message.getParticipants(); 
	gsstl:vector<gsstl::string> removedPlayers = message.getRemovedPlayers(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	}
	...
	GS.SetMessageListener(OnMatchUpdatedMessage);
```

