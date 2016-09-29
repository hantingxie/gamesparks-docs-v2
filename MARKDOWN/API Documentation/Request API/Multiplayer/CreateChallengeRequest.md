
# CreateChallengeRequest


Issues a challenge to a group of players from the currently signed in player.

The endTime field must be present unless the challenge template has an achievement set in the 'First to Achievement' field.

The usersToChallenge field must be present for this request if the acessType is PRIVATE (which is the default).


<a href="https://api.gamesparks.net/#createchallengerequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
accessType | No | string | Who can join this challenge. Either PUBLIC, PRIVATE or FRIENDS
analyticsData | No | AnalyticsData | Optional data used by analytics
autoStartJoinedChallengeOnMaxPlayers | No | boolean | Whether this challenge should automatically start when a new player joins and maxPlayers is reached
challengeMessage | No | string | An optional message to include with the challenge
challengeShortCode | Yes | string | The short code of the challenge
currency1Wager | No | number | The ammount of currency type 1 that the player is wagering on this challenge
currency2Wager | No | number | The amount of currency type 2 that the player is wagering on this challenge
currency3Wager | No | number | The amount of currency type 3 that the player is wagering on this challenge
currency4Wager | No | number | The amount of currency type 4 that the player is wagering on this challenge
currency5Wager | No | number | The amount of currency type 5 that the player is wagering on this challenge
currency6Wager | No | number | The amount of currency type 6 that the player is wagering on this challenge
eligibilityCriteria | No | JSON | Criteria for who can and cannot find and join this challenge (when the accessType is PUBLIC or FRIENDS).
endTime | No | date | The time at which this challenge will end
expiryTime | No | date | The latest time that players can join this challenge
maxAttempts | No | number | The maximum number of attempts 
maxPlayers | No | number | The maximum number of players that are allowed to join this challenge
minPlayers | No | number | The minimum number of players that are allowed to join this challenge
silent | No | boolean | If True  no messaging is triggered
startTime | No | date | The time at which this challenge will begin
usersToChallenge | No | string[] | A player id or an array of player ids who will recieve this challenge

## Response Parameters


A response to a create challenge response

Parameter | Type | Description
--------- | ---- | -----------
challengeInstanceId | string | The challenge instance id
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
challengeInstanceId | INVALID | The ID does not match a challenge the user is involved with
eligibilityCriteria | { "XXX" : "UNRECOGNISED"} | XXX is not a valid field of eligibilityCriteria
eligibilityCriteria | { "segments" : {"XXX" : "MALFORMED"}} | The value provided for XXX is not in the correct format

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new CreateChallengeRequest()
		.SetAccessType(accessType)
		.SetAnalyticsData(analyticsData)
		.SetAutoStartJoinedChallengeOnMaxPlayers(autoStartJoinedChallengeOnMaxPlayers)
		.SetChallengeMessage(challengeMessage)
		.SetChallengeShortCode(challengeShortCode)
		.SetCurrency1Wager(currency1Wager)
		.SetCurrency2Wager(currency2Wager)
		.SetCurrency3Wager(currency3Wager)
		.SetCurrency4Wager(currency4Wager)
		.SetCurrency5Wager(currency5Wager)
		.SetCurrency6Wager(currency6Wager)
		.SetEligibilityCriteria(eligibilityCriteria)
		.SetEndTime(endTime)
		.SetExpiryTime(expiryTime)
		.SetMaxAttempts(maxAttempts)
		.SetMaxPlayers(maxPlayers)
		.SetMinPlayers(minPlayers)
		.SetSilent(silent)
		.SetStartTime(startTime)
		.SetUsersToChallenge(usersToChallenge)
		.Send((response) => {
		string challengeInstanceId = response.ChallengeInstanceId; 
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
	    .createCreateChallengeRequest()
		.setAccessType(accessType)
		.setAnalyticsData(analyticsData)
		.setAutoStartJoinedChallengeOnMaxPlayers(autoStartJoinedChallengeOnMaxPlayers)
		.setChallengeMessage(challengeMessage)
		.setChallengeShortCode(challengeShortCode)
		.setCurrency1Wager(currency1Wager)
		.setCurrency2Wager(currency2Wager)
		.setCurrency3Wager(currency3Wager)
		.setCurrency4Wager(currency4Wager)
		.setCurrency5Wager(currency5Wager)
		.setCurrency6Wager(currency6Wager)
		.setEligibilityCriteria(eligibilityCriteria)
		.setEndTime(endTime)
		.setExpiryTime(expiryTime)
		.setMaxAttempts(maxAttempts)
		.setMaxPlayers(maxPlayers)
		.setMinPlayers(minPlayers)
		.setSilent(silent)
		.setStartTime(startTime)
		.setUsersToChallenge(usersToChallenge)
		.send(function(response:com.gamesparks.api.responses.CreateChallengeResponse):void {
		var challengeInstanceId:String = response.getChallengeInstanceId(); 
		var scriptData:ScriptData = response.getScriptData(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSCreateChallengeRequest* request = [[GSCreateChallengeRequest alloc] init];
	[request setAccessType:accessType;
	[request setAnalyticsData:analyticsData;
	[request setAutoStartJoinedChallengeOnMaxPlayers:autoStartJoinedChallengeOnMaxPlayers;
	[request setChallengeMessage:challengeMessage;
	[request setChallengeShortCode:challengeShortCode;
	[request setCurrency1Wager:currency1Wager;
	[request setCurrency2Wager:currency2Wager;
	[request setCurrency3Wager:currency3Wager;
	[request setCurrency4Wager:currency4Wager;
	[request setCurrency5Wager:currency5Wager;
	[request setCurrency6Wager:currency6Wager;
	[request setEligibilityCriteria:eligibilityCriteria;
	[request setEndTime:endTime;
	[request setExpiryTime:expiryTime;
	[request setMaxAttempts:maxAttempts;
	[request setMaxPlayers:maxPlayers;
	[request setMinPlayers:minPlayers;
	[request setSilent:silent;
	[request setStartTime:startTime;
	[request setUsersToChallenge:usersToChallenge;
	[request setCallback:^ (GSCreateChallengeResponse* response) {
	NSString* challengeInstanceId = [response getChallengeInstanceId]; 
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
	
	void CreateChallengeRequest_Response(GS& gsInstance, const CreateChallengeResponse& response) {
	gsstl::string challengeInstanceId = response.getChallengeInstanceId(); 
	GSData scriptData = response.getScriptData(); 
	}
	......
	
	CreateChallengeRequest request(gsInstance);
	request.SetAccessType(accessType)
	request.SetAnalyticsData(analyticsData)
	request.SetAutoStartJoinedChallengeOnMaxPlayers(autoStartJoinedChallengeOnMaxPlayers)
	request.SetChallengeMessage(challengeMessage)
	request.SetChallengeShortCode(challengeShortCode)
	request.SetCurrency1Wager(currency1Wager)
	request.SetCurrency2Wager(currency2Wager)
	request.SetCurrency3Wager(currency3Wager)
	request.SetCurrency4Wager(currency4Wager)
	request.SetCurrency5Wager(currency5Wager)
	request.SetCurrency6Wager(currency6Wager)
	request.SetEligibilityCriteria(eligibilityCriteria)
	request.SetEndTime(endTime)
	request.SetExpiryTime(expiryTime)
	request.SetMaxAttempts(maxAttempts)
	request.SetMaxPlayers(maxPlayers)
	request.SetMinPlayers(minPlayers)
	request.SetSilent(silent)
	request.SetStartTime(startTime)
	request.SetUsersToChallenge(usersToChallenge)
	request.Send(CreateChallengeRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.CreateChallengeRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.CreateChallengeResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createCreateChallengeRequest()
	.setAccessType(accessType)
	.setAnalyticsData(analyticsData)
	.setAutoStartJoinedChallengeOnMaxPlayers(autoStartJoinedChallengeOnMaxPlayers)
	.setChallengeMessage(challengeMessage)
	.setChallengeShortCode(challengeShortCode)
	.setCurrency1Wager(currency1Wager)
	.setCurrency2Wager(currency2Wager)
	.setCurrency3Wager(currency3Wager)
	.setCurrency4Wager(currency4Wager)
	.setCurrency5Wager(currency5Wager)
	.setCurrency6Wager(currency6Wager)
	.setEligibilityCriteria(eligibilityCriteria)
	.setEndTime(endTime)
	.setExpiryTime(expiryTime)
	.setMaxAttempts(maxAttempts)
	.setMaxPlayers(maxPlayers)
	.setMinPlayers(minPlayers)
	.setSilent(silent)
	.setStartTime(startTime)
	.setUsersToChallenge(usersToChallenge)
	.send(new GSEventListener<CreateChallengeResponse>() {
		@Override
		public void onEvent(CreateChallengeResponse response) {
			String challengeInstanceId = response.getChallengeInstanceId(); 
			GSData scriptData = response.getScriptData(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.CreateChallengeRequest();
	request.accessType = ...;
	request.analyticsData = ...;
	request.autoStartJoinedChallengeOnMaxPlayers = ...;
	request.challengeMessage = ...;
	request.challengeShortCode = ...;
	request.currency1Wager = ...;
	request.currency2Wager = ...;
	request.currency3Wager = ...;
	request.currency4Wager = ...;
	request.currency5Wager = ...;
	request.currency6Wager = ...;
	request.eligibilityCriteria = ...;
	request.endTime = ...;
	request.expiryTime = ...;
	request.maxAttempts = ...;
	request.maxPlayers = ...;
	request.minPlayers = ...;
	request.silent = ...;
	request.startTime = ...;
	request.usersToChallenge = ...;
	var response = request.Send();
	
var challengeInstanceId = response.challengeInstanceId; 
var scriptData = response.scriptData; 
```


