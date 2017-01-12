
# ChallengeJoinedMessage


A message indicating that the challenge has been joined.


<a href="https://api.gamesparks.net/#challengejoinedmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challenge | No | Challenge | An object representing the challenge.
message | No | string | A player message included in this message.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.
who | No | string | The name of the player whose actions generated this message.

## Nested types

### PlayerDetail

An object representing a player's id and name

Parameter | Type | Description
--------- | ---- | -----------
externalIds | JSON | A player's external identifiers
id | string | A player's id
name | string | A player's name

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


## Code Samples

<h3>C#</h3>
```cs
	ChallengeJoinedMessage.Listener = (message) => {
	var challenge = message.Challenge; 
	string message = message.Message; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	string who = message.Who; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".ChallengeJoinedMessage",
		function (message:ChallengeJoinedMessage):void {
		var challenge:Challenge = message.getChallenge(); 
		var message:String = message.getMessage(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		var who:String = message.getWho(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSChallengeJoinedMessage:^(GSChallengeJoinedMessage* message) {
	GSChallenge* challenge = [message getChallenge]; 
	NSString* message = [message getMessage]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	NSString* who = [message getWho]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setChallengeJoinedMessageListener(
		new GSEventConsumer<ChallengeJoinedMessage>() {
			public void onEvent(ChallengeJoinedMessage event) {
		Challenge challenge = message.getChallenge(); 
		String message = message.getMessage(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String title = message.getTitle(); 
		String who = message.getWho(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnChallengeJoinedMessage(GS& gsInstance, const ChallengeJoinedMessage& message)
	{
	Types::Challenge* challenge = message.getChallenge(); 
	gsstl::string message = message.getMessage(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	gsstl::string who = message.getWho(); 
	}
	...
	GS.SetMessageListener(OnChallengeJoinedMessage);
```

