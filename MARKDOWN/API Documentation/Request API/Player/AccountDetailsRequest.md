---
src: /API Documentation/Request API/Player/AccountDetailsRequest.md
---

# AccountDetailsRequest


Retrieves the details of the current authenticated player.


<a href="https://api.gamesparks.net/#accountdetailsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------

## Response Parameters


A response containing the player's data.

Parameter | Type | Description
--------- | ---- | -----------
achievements | string[] | A JSON object containing the player's achievments
currency1 | number | The amount of type 1 currency that the player holds
currency2 | number | The amount of type 2 currency that the player holds
currency3 | number | The amount of type 3 currency that the player holds
currency4 | number | The amount of type 4 currency that the player holds
currency5 | number | The amount of type 5 currency that the player holds
currency6 | number | The amount of type 6 currency that the player holds
displayName | string | The player's display name
externalIds | JSON | A JSON object containing the player's external account details
location | [Location](#location) | A JSON object containing the player's location
reservedCurrency1 | JSON | The amount of type 1 currency that the player holds which is currently reserved
reservedCurrency2 | JSON | The amount of type 2 currency that the player holds which is currently reserved
reservedCurrency3 | JSON | The amount of type 3 currency that the player holds which is currently reserved
reservedCurrency4 | JSON | The amount of type 4 currency that the player holds which is currently reserved
reservedCurrency5 | JSON | The amount of type 5 currency that the player holds which is currently reserved
reservedCurrency6 | JSON | The amount of type 6 currency that the player holds which is currently reserved
userId | string | The player's id
virtualGoods | JSON | A JSON object containing the virtual goods that the player owns

## Nested types

### Location

Location details.

Parameter | Type | Description
--------- | ---- | -----------
city | string | The city
country | string | The country
latitide | Float | The latitude
longditute | Float | The longditute


## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new AccountDetailsRequest()
		.Send((response) => {
		IList<string> achievements = response.Achievements; 
		long? currency1 = response.Currency1; 
		long? currency2 = response.Currency2; 
		long? currency3 = response.Currency3; 
		long? currency4 = response.Currency4; 
		long? currency5 = response.Currency5; 
		long? currency6 = response.Currency6; 
		string displayName = response.DisplayName; 
		GSData externalIds = response.ExternalIds; 
		var location = response.Location; 
		GSData reservedCurrency1 = response.ReservedCurrency1; 
		GSData reservedCurrency2 = response.ReservedCurrency2; 
		GSData reservedCurrency3 = response.ReservedCurrency3; 
		GSData reservedCurrency4 = response.ReservedCurrency4; 
		GSData reservedCurrency5 = response.ReservedCurrency5; 
		GSData reservedCurrency6 = response.ReservedCurrency6; 
		string userId = response.UserId; 
		GSData virtualGoods = response.VirtualGoods; 
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
	    .createAccountDetailsRequest()
		.send(function(response:com.gamesparks.api.responses.AccountDetailsResponse):void {
		var achievements:Vector.<String> = response.getAchievements(); 
		var currency1:Number = response.getCurrency1(); 
		var currency2:Number = response.getCurrency2(); 
		var currency3:Number = response.getCurrency3(); 
		var currency4:Number = response.getCurrency4(); 
		var currency5:Number = response.getCurrency5(); 
		var currency6:Number = response.getCurrency6(); 
		var displayName:String = response.getDisplayName(); 
		var externalIds:Object = response.getExternalIds(); 
		var location:Location = response.getLocation(); 
		var reservedCurrency1:Object = response.getReservedCurrency1(); 
		var reservedCurrency2:Object = response.getReservedCurrency2(); 
		var reservedCurrency3:Object = response.getReservedCurrency3(); 
		var reservedCurrency4:Object = response.getReservedCurrency4(); 
		var reservedCurrency5:Object = response.getReservedCurrency5(); 
		var reservedCurrency6:Object = response.getReservedCurrency6(); 
		var userId:String = response.getUserId(); 
		var virtualGoods:Object = response.getVirtualGoods(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSAccountDetailsRequest* request = [[GSAccountDetailsRequest alloc] init];
	[request setCallback:^ (GSAccountDetailsResponse* response) {
	NSArray* achievements = [response getAchievements]; 
	NSNumber* currency1 = [response getCurrency1]; 
	NSNumber* currency2 = [response getCurrency2]; 
	NSNumber* currency3 = [response getCurrency3]; 
	NSNumber* currency4 = [response getCurrency4]; 
	NSNumber* currency5 = [response getCurrency5]; 
	NSNumber* currency6 = [response getCurrency6]; 
	NSString* displayName = [response getDisplayName]; 
	NSDictionary* externalIds = [response getExternalIds]; 
	GSLocation* location = [response getLocation]; 
	NSDictionary* reservedCurrency1 = [response getReservedCurrency1]; 
	NSDictionary* reservedCurrency2 = [response getReservedCurrency2]; 
	NSDictionary* reservedCurrency3 = [response getReservedCurrency3]; 
	NSDictionary* reservedCurrency4 = [response getReservedCurrency4]; 
	NSDictionary* reservedCurrency5 = [response getReservedCurrency5]; 
	NSDictionary* reservedCurrency6 = [response getReservedCurrency6]; 
	NSString* userId = [response getUserId]; 
	NSDictionary* virtualGoods = [response getVirtualGoods]; 
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
	
	void AccountDetailsRequest_Response(GS& gsInstance, const AccountDetailsResponse& response) {
	gsstl:vector<gsstl::string> achievements = response.getAchievements(); 
	Optional::t_LongOptional currency1 = response.getCurrency1(); 
	Optional::t_LongOptional currency2 = response.getCurrency2(); 
	Optional::t_LongOptional currency3 = response.getCurrency3(); 
	Optional::t_LongOptional currency4 = response.getCurrency4(); 
	Optional::t_LongOptional currency5 = response.getCurrency5(); 
	Optional::t_LongOptional currency6 = response.getCurrency6(); 
	gsstl::string displayName = response.getDisplayName(); 
	GSData externalIds = response.getExternalIds(); 
	Types::Location* location = response.getLocation(); 
	GSData reservedCurrency1 = response.getReservedCurrency1(); 
	GSData reservedCurrency2 = response.getReservedCurrency2(); 
	GSData reservedCurrency3 = response.getReservedCurrency3(); 
	GSData reservedCurrency4 = response.getReservedCurrency4(); 
	GSData reservedCurrency5 = response.getReservedCurrency5(); 
	GSData reservedCurrency6 = response.getReservedCurrency6(); 
	gsstl::string userId = response.getUserId(); 
	GSData virtualGoods = response.getVirtualGoods(); 
	}
	......
	
	AccountDetailsRequest request(gsInstance);
	request.Send(AccountDetailsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.AccountDetailsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.AccountDetailsResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createAccountDetailsRequest()
	.send(new GSEventListener<AccountDetailsResponse>() {
		@Override
		public void onEvent(AccountDetailsResponse response) {
			List<String> achievements = response.getAchievements(); 
			Long currency1 = response.getCurrency1(); 
			Long currency2 = response.getCurrency2(); 
			Long currency3 = response.getCurrency3(); 
			Long currency4 = response.getCurrency4(); 
			Long currency5 = response.getCurrency5(); 
			Long currency6 = response.getCurrency6(); 
			String displayName = response.getDisplayName(); 
			GSData externalIds = response.getExternalIds(); 
			Location location = response.getLocation(); 
			GSData reservedCurrency1 = response.getReservedCurrency1(); 
			GSData reservedCurrency2 = response.getReservedCurrency2(); 
			GSData reservedCurrency3 = response.getReservedCurrency3(); 
			GSData reservedCurrency4 = response.getReservedCurrency4(); 
			GSData reservedCurrency5 = response.getReservedCurrency5(); 
			GSData reservedCurrency6 = response.getReservedCurrency6(); 
			String userId = response.getUserId(); 
			GSData virtualGoods = response.getVirtualGoods(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.AccountDetailsRequest();
	var response = request.Send();
	
var achievements = response.achievements; 
var currency1 = response.currency1; 
var currency2 = response.currency2; 
var currency3 = response.currency3; 
var currency4 = response.currency4; 
var currency5 = response.currency5; 
var currency6 = response.currency6; 
var displayName = response.displayName; 
var externalIds = response.externalIds; 
var location = response.location; 
var reservedCurrency1 = response.reservedCurrency1; 
var reservedCurrency2 = response.reservedCurrency2; 
var reservedCurrency3 = response.reservedCurrency3; 
var reservedCurrency4 = response.reservedCurrency4; 
var reservedCurrency5 = response.reservedCurrency5; 
var reservedCurrency6 = response.reservedCurrency6; 
var userId = response.userId; 
var virtualGoods = response.virtualGoods; 
```


