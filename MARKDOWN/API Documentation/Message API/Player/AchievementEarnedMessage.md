
# AchievementEarnedMessage


Message sent to a player when they have been awarded an achievement within the game.

This message may be triggered by a leaderboard or a script.

The player may have gained a virtual good or virtual currency as a result of gaining the award.


<a href="https://api.gamesparks.net/#achievementearnedmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
achievementName | No | string | The name of achievement.
achievementShortCode | No | string | The short code of the achievement.
currency1Earned | No | string | The amount of type 1 currency earned.
currency2Earned | No | string | The amount of type 2 currency earned.
currency3Earned | No | string | The amount of type 2 currency earned.
currency4Earned | No | string | The amount of type 4 currency earned.
currency5Earned | No | string | The amount of type 5 currency earned.
currency6Earned | No | string | The amount of type 6 currency earned.
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.
virtualGoodEarned | No | string | The name of the virtual good that was earned.

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
	AchievementEarnedMessage.Listener = (message) => {
	string achievementName = message.AchievementName; 
	string achievementShortCode = message.AchievementShortCode; 
	string currency1Earned = message.Currency1Earned; 
	string currency2Earned = message.Currency2Earned; 
	string currency3Earned = message.Currency3Earned; 
	string currency4Earned = message.Currency4Earned; 
	string currency5Earned = message.Currency5Earned; 
	string currency6Earned = message.Currency6Earned; 
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	string virtualGoodEarned = message.VirtualGoodEarned; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".AchievementEarnedMessage",
		function (message:AchievementEarnedMessage):void {
		var achievementName:String = message.getAchievementName(); 
		var achievementShortCode:String = message.getAchievementShortCode(); 
		var currency1Earned:String = message.getCurrency1Earned(); 
		var currency2Earned:String = message.getCurrency2Earned(); 
		var currency3Earned:String = message.getCurrency3Earned(); 
		var currency4Earned:String = message.getCurrency4Earned(); 
		var currency5Earned:String = message.getCurrency5Earned(); 
		var currency6Earned:String = message.getCurrency6Earned(); 
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		var virtualGoodEarned:String = message.getVirtualGoodEarned(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSAchievementEarnedMessage:^(GSAchievementEarnedMessage* message) {
	NSString* achievementName = [message getAchievementName]; 
	NSString* achievementShortCode = [message getAchievementShortCode]; 
	NSString* currency1Earned = [message getCurrency1Earned]; 
	NSString* currency2Earned = [message getCurrency2Earned]; 
	NSString* currency3Earned = [message getCurrency3Earned]; 
	NSString* currency4Earned = [message getCurrency4Earned]; 
	NSString* currency5Earned = [message getCurrency5Earned]; 
	NSString* currency6Earned = [message getCurrency6Earned]; 
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	NSString* virtualGoodEarned = [message getVirtualGoodEarned]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setAchievementEarnedMessageListener(
		new GSEventConsumer<AchievementEarnedMessage>() {
			public void onEvent(AchievementEarnedMessage event) {
		String achievementName = message.getAchievementName(); 
		String achievementShortCode = message.getAchievementShortCode(); 
		String currency1Earned = message.getCurrency1Earned(); 
		String currency2Earned = message.getCurrency2Earned(); 
		String currency3Earned = message.getCurrency3Earned(); 
		String currency4Earned = message.getCurrency4Earned(); 
		String currency5Earned = message.getCurrency5Earned(); 
		String currency6Earned = message.getCurrency6Earned(); 
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String title = message.getTitle(); 
		String virtualGoodEarned = message.getVirtualGoodEarned(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnAchievementEarnedMessage(GS& gsInstance, const AchievementEarnedMessage& message)
	{
	gsstl::string achievementName = message.getAchievementName(); 
	gsstl::string achievementShortCode = message.getAchievementShortCode(); 
	gsstl::string currency1Earned = message.getCurrency1Earned(); 
	gsstl::string currency2Earned = message.getCurrency2Earned(); 
	gsstl::string currency3Earned = message.getCurrency3Earned(); 
	gsstl::string currency4Earned = message.getCurrency4Earned(); 
	gsstl::string currency5Earned = message.getCurrency5Earned(); 
	gsstl::string currency6Earned = message.getCurrency6Earned(); 
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	gsstl::string virtualGoodEarned = message.getVirtualGoodEarned(); 
	}
	...
	GS.SetMessageListener(OnAchievementEarnedMessage);
```

