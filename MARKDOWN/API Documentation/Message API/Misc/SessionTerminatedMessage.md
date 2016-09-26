---
src: /API Documentation/Message API/Misc/SessionTerminatedMessage.md
---

# SessionTerminatedMessage


A message sent to sockets when disconnectOthers() has been called.


<a href="https://api.gamesparks.net/#sessionterminatedmessage" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
authToken | No | string | Used to automatically re-authenticate a client during socket connect.



## Code Samples

<h3>C#</h3>
```cs
	SessionTerminatedMessage.Listener = (message) => {
	string authToken = message.AuthToken; 
	};

```
### ActionScript 3
```actionscript
	gs.getMessageHandler().setHandler(
		".SessionTerminatedMessage",
		function (message:SessionTerminatedMessage):void {
		var authToken:String = message.getAuthToken(); 
		}
);

```
### Objective-C
```objectivec
	[listener onGSSessionTerminatedMessage:^(GSSessionTerminatedMessage* message) {
	NSString* authToken = [message getAuthToken]; 
	}];

```
### Java
```java
	gs.getMessageHandler().setSessionTerminatedMessageListener(
		new GSEventConsumer<SessionTerminatedMessage>() {
			public void onEvent(SessionTerminatedMessage event) {
		String authToken = message.getAuthToken(); 
			}
		}
	);
```
### C++
```cpp
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Messages;
	...
	void OnSessionTerminatedMessage(GS& gsInstance, const SessionTerminatedMessage& message)
	{
	gsstl::string authToken = message.getAuthToken(); 
	}
	...
	GS.SetMessageListener(OnSessionTerminatedMessage);
```

