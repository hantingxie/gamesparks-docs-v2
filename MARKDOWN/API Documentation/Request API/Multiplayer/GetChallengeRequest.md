---
src: /API Documentation/Request API/Multiplayer/GetChallengeRequest.md
---

# GetChallengeRequest


Gets the details of a challenge. The current player must be involved in the challenge for the request to succeed.


<a href="https://api.gamesparks.net/#getchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
challengeInstanceId | Yes | string | The ID of the challenge
message | No | string | An optional message to send with the challenge

## Response Parameters


A response containing the details of a challenge

Parameter | Type | Description
--------- | ---- | -----------
challenge | [Challenge](#challenge) | A JSON object representing the challenge.
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

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

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
challengeInstanceId | INVALID | The supplied challengeInstanceId does not match a challenge related to the current player

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new GetChallengeRequest()
		.SetChallengeInstanceId(challengeInstanceId)
		.SetMessage(message)
		.Send((response) => {
		var challenge = response.Challenge; 
		GSData scriptData = response.ScriptData; 
		});

```

### ActionScript 3
```actionscript
	import com.gamesparks.*;
	import com.gamesparks.api.requests.*;
	import com.gamesparks.api.responses.*;
	import com.gamesparks.api.types.*;
	...
	
	gs.getRequestBuilder()
	    .createGetChallengeRequest()
		.setChallengeInstanceId(challengeInstanceId)
		.setMessage(message)
		.send(function(response:com.gamesparks.api.responses.GetChallengeResponse):void {
		var challenge:Challenge = response.getChallenge(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSGetChallengeRequest* request = [[GSGetChallengeRequest alloc] init];
	[request setChallengeInstanceId:challengeInstanceId;
	[request setMessage:message;
	[request setCallback:^ (GSGetChallengeResponse* response) {
	GSChallenge* challenge = [response getChallenge]; 
	NSDictionary* scriptData = [response getScriptData]; 
	}];
	[gs send:request];

```

### C++
```cpp

	#include <GameSparks/generated/GSRequests.h>
	using namespace GameSparks::Core;
	using namespace GameSparks::Api::Responses;
	using namespace GameSparks::Api::Requests;
	...
	
	void GetChallengeRequest_Response(GS& gsInstance, const GetChallengeResponse& response) {
	Types::Challenge* challenge = response.getChallenge(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	GetChallengeRequest request(gsInstance);
	request.SetChallengeInstanceId(challengeInstanceId)
	request.SetMessage(message)
	request.Send(GetChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.GetChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.GetChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createGetChallengeRequest()
	.setChallengeInstanceId(challengeInstanceId)
	.setMessage(message)
	.send(new GSEventListener<GetChallengeResponse>() {
		@Override
		public void onEvent(GetChallengeResponse response) {
			Challenge challenge = response.getChallenge(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.GetChallengeRequest();
	request.challengeInstanceId = ...;
	request.message = ...;
	var response = request.Send();
	
var challenge = response.challenge; 
var scriptData = response.scriptData; 
```


