---
src: /API Documentation/Message API/Teams/TeamChatMessage.md
---

# TeamChatMessage


A message sent from a player to an entire team.


<a href="https://api.gamesparks.net/#teamchatmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
chatMessageId | No | string | The identifier for this message as it appears in the chat history.
fromId | No | string | The player's id who is sending the message.
message | No | string | The message to send to the team.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
ownerId | No | string | The id of the owner
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
teamId | No | string | The id of the team
teamType | No | string | The team type
title | No | string | A textual title for the message.
who | No | string | The name of the player who is sending the message.

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.


## Code Samples

<h3>C#</h3>
```cs
	TeamChatMessage.Listener = (message) => {
	string chatMessageId = message.ChatMessageId; 
	string fromId = message.FromId; 
	string message = message.Message; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	string ownerId = message.OwnerId; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string teamId = message.TeamId; 
	string teamType = message.TeamType; 
	string title = message.Title; 
	string who = message.Who; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".TeamChatMessage",
		function (message:TeamChatMessage):void {
		var chatMessageId:String = message.getChatMessageId(); 
		var fromId:String = message.getFromId(); 
		var message:String = message.getMessage(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var ownerId:String = message.getOwnerId(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var teamId:String = message.getTeamId(); 
		var teamType:String = message.getTeamType(); 
		var title:String = message.getTitle(); 
		var who:String = message.getWho(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSTeamChatMessage:^(GSTeamChatMessage* message) {
	NSString* chatMessageId = [message getChatMessageId]; 
	NSString* fromId = [message getFromId]; 
	NSString* message = [message getMessage]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSString* ownerId = [message getOwnerId]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* teamId = [message getTeamId]; 
	NSString* teamType = [message getTeamType]; 
	NSString* title = [message getTitle]; 
	NSString* who = [message getWho]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setTeamChatMessageListener(
		new GSEventConsumer<TeamChatMessage>() {
			public void onEvent(TeamChatMessage event) {
		String chatMessageId = message.getChatMessageId(); 
		String fromId = message.getFromId(); 
		String message = message.getMessage(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		String ownerId = message.getOwnerId(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String teamId = message.getTeamId(); 
		String teamType = message.getTeamType(); 
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
	void OnTeamChatMessage(GS& gsInstance, const TeamChatMessage& message)
	{
	gsstl::string chatMessageId = message.getChatMessageId(); 
	gsstl::string fromId = message.getFromId(); 
	gsstl::string message = message.getMessage(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl::string ownerId = message.getOwnerId(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string teamId = message.getTeamId(); 
	gsstl::string teamType = message.getTeamType(); 
	gsstl::string title = message.getTitle(); 
	gsstl::string who = message.getWho(); 
	}
	...
	GS.SetMessageListener(OnTeamChatMessage);
```

