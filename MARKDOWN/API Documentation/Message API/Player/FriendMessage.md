---
src: /API Documentation/Message API/Player/FriendMessage.md
---

# FriendMessage


A message sent from a player to one of his social network friends.


<a href="https://api.gamesparks.net/#friendmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
fromId | No | string | The player's id who is sending the message.
message | No | string | The player's message.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
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
	FriendMessage.Listener = (message) => {
	string fromId = message.FromId; 
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
		".FriendMessage",
		function (message:FriendMessage):void {
		var fromId:String = message.getFromId(); 
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
	[listener onGSFriendMessage:^(GSFriendMessage* message) {
	NSString* fromId = [message getFromId]; 
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
	gs.getMessageHandler().setFriendMessageListener(
		new GSEventConsumer<FriendMessage>() {
			public void onEvent(FriendMessage event) {
		String fromId = message.getFromId(); 
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
	void OnFriendMessage(GS& gsInstance, const FriendMessage& message)
	{
	gsstl::string fromId = message.getFromId(); 
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
	GS.SetMessageListener(OnFriendMessage);
```

