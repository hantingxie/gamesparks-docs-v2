
# UploadCompleteMessage


A message indicating that the asynchronous upload task trigger by the player is now complete.


<a href="https://api.gamesparks.net/#uploadcompletemessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
messageId | No | string | A unique identifier for this message.
notification | No | boolean | Flag indicating whether this message could be sent as a push notification or not.
scriptData | No | ScriptData[] | ScriptData is arbitrary data that can be stored in a message by a Cloud Code script.
subTitle | No | string | A textual title for the message.
summary | No | string | A textual summary describing the message's purpose.
title | No | string | A textual title for the message.
uploadData | No | UploadData | The upload data (if supplied as part of GetUploadUrlRequest) of UploadData objects
uploadId | No | string | The id of the upload

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### UploadData

This object represents the result of uploading a file to the GameSparks platform.

Parameter | Type | Description
--------- | ---- | -----------
fileName | string | The filename of the file that was uploaded.
playerId | string | The unique player id of the player that uploaded the file.


## Code Samples

<h3>C#</h3>
```cs
	UploadCompleteMessage.Listener = (message) => {
	string messageId = message.MessageId; 
	bool? notification = message.Notification; 
	GSEnumerable<GSData> scriptData = message.ScriptData; 
	string subTitle = message.SubTitle; 
	string summary = message.Summary; 
	string title = message.Title; 
	GSData uploadData = message.UploadData; 
	string uploadId = message.UploadId; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".UploadCompleteMessage",
		function (message:UploadCompleteMessage):void {
		var messageId:String = message.getMessageId(); 
		var notification:Boolean = message.getNotification(); 
		var scriptData:Vector.<ScriptData> = message.getScriptData(); 
		var subTitle:String = message.getSubTitle(); 
		var summary:String = message.getSummary(); 
		var title:String = message.getTitle(); 
		var uploadData:UploadData = message.getUploadData(); 
		var uploadId:String = message.getUploadId(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSUploadCompleteMessage:^(GSUploadCompleteMessage* message) {
	NSString* messageId = [message getMessageId]; 
	BOOL notification = [message getNotification]; 
	NSArray* scriptData = [message getScriptData]; 
	NSString* subTitle = [message getSubTitle]; 
	NSString* summary = [message getSummary]; 
	NSString* title = [message getTitle]; 
	NSDictionary* uploadData = [message getUploadData]; 
	NSString* uploadId = [message getUploadId]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setUploadCompleteMessageListener(
		new GSEventConsumer<UploadCompleteMessage>() {
			public void onEvent(UploadCompleteMessage event) {
		String messageId = message.getMessageId(); 
		Boolean notification = message.getNotification(); 
		List<GSData> scriptData = message.getScriptData(); 
		String subTitle = message.getSubTitle(); 
		String summary = message.getSummary(); 
		String title = message.getTitle(); 
		GSData uploadData = message.getUploadData(); 
		String uploadId = message.getUploadId(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnUploadCompleteMessage(GS& gsInstance, const UploadCompleteMessage& message)
	{
	gsstl::string messageId = message.getMessageId(); 
	Optional::t_BoolOptional notification = message.getNotification(); 
	gsstl:vector<GSData> scriptData = message.getScriptData(); 
	gsstl::string subTitle = message.getSubTitle(); 
	gsstl::string summary = message.getSummary(); 
	gsstl::string title = message.getTitle(); 
	GSData uploadData = message.getUploadData(); 
	gsstl::string uploadId = message.getUploadId(); 
	}
	...
	GS.SetMessageListener(OnUploadCompleteMessage);
```

