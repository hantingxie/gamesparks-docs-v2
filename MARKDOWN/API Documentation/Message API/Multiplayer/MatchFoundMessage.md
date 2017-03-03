---
src: /API Documentation/Message API/Multiplayer/MatchFoundMessage.md
---

# MatchFoundMessage


A message indicating that a match has been found


<a href="https://api.gamesparks.net/#matchfoundmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
accessToken | No | string | The accessToken used to authenticate this player for this match
host | No | string | The host to connect to for this match
matchData | No | JSON | MatchData is arbitrary data that can be stored in a Match instance by a Cloud Code script.
matchGroup | No | string | The group the player was assigned in the matchmaking request
matchId | No | string | The id for this match instance
matchShortCode | No | string | The shortCode of the match type this message for
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
participants | No | Participant[] | The participants in this match
port | No | number | The port to connect to for this match
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


## Code Samples

<h3>C#</h3>
```cs
	MatchFoundMessage.Listener = (message) => {
	string accessToken = message.AccessToken; 
	string host = message.Host; 
	GSData matchData = message.MatchData; 
	string matchGroup = message.MatchGroup; 
	string matchId = message.MatchId; 
	string matchShortCode = message.MatchShortCode; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<var> participants = message.Participants; 
	int? port = message.Port; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".MatchFoundMessage",
		function (message:MatchFoundMessage):void {
		var accessToken:String = message.getAccessToken(); 
		var host:String = message.getHost(); 
		var matchData:Object = message.getMatchData(); 
		var matchGroup:String = message.getMatchGroup(); 
		var matchId:String = message.getMatchId(); 
		var matchShortCode:String = message.getMatchShortCode(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var participants:Vector.<Participant> = message.getParticipants(); 
		var port:Number = message.getPort(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSMatchFoundMessage:^(GSMatchFoundMessage* message) {
	NSString* accessToken = [message getAccessToken]; 
	NSString* host = [message getHost]; 
	NSDictionary* matchData = [message getMatchData]; 
	NSString* matchGroup = [message getMatchGroup]; 
	NSString* matchId = [message getMatchId]; 
	NSString* matchShortCode = [message getMatchShortCode]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* participants = [message getParticipants]; 
	NSNumber* port = [message getPort]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setMatchFoundMessageListener(
		new GSEventConsumer<MatchFoundMessage>() {
			public void onEvent(MatchFoundMessage event) {
		String accessToken = message.getAccessToken(); 
		String host = message.getHost(); 
		GSData matchData = message.getMatchData(); 
		String matchGroup = message.getMatchGroup(); 
		String matchId = message.getMatchId(); 
		String matchShortCode = message.getMatchShortCode(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<Participant> participants = message.getParticipants(); 
		Integer port = message.getPort(); 
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
	void OnMatchFoundMessage(GS& gsInstance, const MatchFoundMessage& message)
	{
	gsstl::string accessToken = message.getAccessToken(); 
	gsstl::string host = message.getHost(); 
	GSData matchData = message.getMatchData(); 
	gsstl::string matchGroup = message.getMatchGroup(); 
	gsstl::string matchId = message.getMatchId(); 
	gsstl::string matchShortCode = message.getMatchShortCode(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<Types::Participant*> participants = message.getParticipants(); 
	Optional::t_LongOptional port = message.getPort(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	}
	...
	GS.SetMessageListener(OnMatchFoundMessage);
```

