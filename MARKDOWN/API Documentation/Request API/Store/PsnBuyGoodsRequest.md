---
src: /API Documentation/Request API/Store/PsnBuyGoodsRequest.md
---

# PsnBuyGoodsRequest


Processes an update of entitlement in PlayStation network.

The GameSparks platform will update the 'use_count' for an entitlement (by default 'use_count' is 1).

The request will be rejected if entitlement 'use_limit' is 0

GampSparks platform by default will use internally saved PSN user access token


<a href="https://api.gamesparks.net/#psnbuygoodsrequest" target="_gsapi">View interactive version here</a>

## Request Parameters

Parameter | Required | Type | Description
--------- | -------- | ---- | -----------
analyticsData | No | AnalyticsData | Optional data used by analytics
authorizationCode | No | string | The authorization code obtained from PSN, as described here https://ps4.scedev.net/resources/documents/SDK/latest/NpAuth-Reference/0008.html
entitlementLabel | Yes | string | Specify the entitlement label of the entitlement to update. (Not an entitlement ID).
redirectUri | No | string | When using the authorization code obtained from PlayStation®4/PlayStation®Vita/PlayStation®3, this is not required.
uniqueTransactionByPlayer | No | boolean | If set to true, the transactionId from this receipt will not be globally valdidated, this will mean replays between players are possible.
useCount | No | number | Optional - specify the quantity of the entitlement to use. Default = 1

## Response Parameters


A response containing details of the bought items

Parameter | Type | Description
--------- | ---- | -----------
boughtItems | [Boughtitem[]](#boughtitem) | A JSON object containing details of the bought items
currency1Added | number | How much currency type 1 was added
currency2Added | number | How much currency type 2 was added
currency3Added | number | How much currency type 3 was added
currency4Added | number | How much currency type 4 was added
currency5Added | number | How much currency type 5 was added
currency6Added | number | How much currency type 6 was added
currencyConsumed | number | For a buy with currency request, how much currency was used
currencyType | number | For a buy with currency request, which currency type was used
scriptData | ScriptData | A JSON Map of any data added either to the Request or the Response by your Cloud Code
transactionIds | string[] | The list of transactionIds, for this purchase, if they exist. This field is populated only for store buys

## Nested types

### ScriptData

A collection of arbitrary data that can be added to a message via a Cloud Code script.

Parameter | Type | Description
--------- | ---- | -----------
myKey | string | An arbitrary data key
myValue | JSON | An arbitrary data value.

### Boughtitem

A nested object that represents a bought item.

Parameter | Type | Description
--------- | ---- | -----------
quantity | number | The quantity of the bought item
shortCode | string | The short code of the bought item

## Error Codes

Key | Value | Description
--------- | ----------- | -----------
verificationError | 1 | No matching virtual good can be found
verificationError | 2 | The PSN servers failed to verify the entitlementLabel
verificationError | 3 | There was an error connecting to the PSN server

## Code Samples

<h3>C#</h3>
```cs
	using GameSparks.Api;
	using GameSparks.Api.Requests;
	using GameSparks.Api.Responses;
	...
	new PsnBuyGoodsRequest()
		.SetAnalyticsData(analyticsData)
		.SetAuthorizationCode(authorizationCode)
		.SetEntitlementLabel(entitlementLabel)
		.SetRedirectUri(redirectUri)
		.SetUniqueTransactionByPlayer(uniqueTransactionByPlayer)
		.SetUseCount(useCount)
		.Send((response) => {
		GSEnumerable<var> boughtItems = response.BoughtItems; 
		long? currency1Added = response.Currency1Added; 
		long? currency2Added = response.Currency2Added; 
		long? currency3Added = response.Currency3Added; 
		long? currency4Added = response.Currency4Added; 
		long? currency5Added = response.Currency5Added; 
		long? currency6Added = response.Currency6Added; 
		long? currencyConsumed = response.CurrencyConsumed; 
		int? currencyType = response.CurrencyType; 
		GSData scriptData = response.ScriptData; 
		IList<string> transactionIds = response.TransactionIds; 
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
	    .createPsnBuyGoodsRequest()
		.setAnalyticsData(analyticsData)
		.setAuthorizationCode(authorizationCode)
		.setEntitlementLabel(entitlementLabel)
		.setRedirectUri(redirectUri)
		.setUniqueTransactionByPlayer(uniqueTransactionByPlayer)
		.setUseCount(useCount)
		.send(function(response:com.gamesparks.api.responses.BuyVirtualGoodResponse):void {
		var boughtItems:Vector.<Boughtitem> = response.getBoughtItems(); 
		var currency1Added:Number = response.getCurrency1Added(); 
		var currency2Added:Number = response.getCurrency2Added(); 
		var currency3Added:Number = response.getCurrency3Added(); 
		var currency4Added:Number = response.getCurrency4Added(); 
		var currency5Added:Number = response.getCurrency5Added(); 
		var currency6Added:Number = response.getCurrency6Added(); 
		var currencyConsumed:Number = response.getCurrencyConsumed(); 
		var currencyType:Number = response.getCurrencyType(); 
		var scriptData:ScriptData = response.getScriptData(); 
		var transactionIds:Vector.<String> = response.getTransactionIds(); 
		});

```

### Objective-C
```objectivec
	#import "GS.h"
	#import "GSAPI.h"
	...
	GSPsnBuyGoodsRequest* request = [[GSPsnBuyGoodsRequest alloc] init];
	[request setAnalyticsData:analyticsData;
	[request setAuthorizationCode:authorizationCode;
	[request setEntitlementLabel:entitlementLabel;
	[request setRedirectUri:redirectUri;
	[request setUniqueTransactionByPlayer:uniqueTransactionByPlayer;
	[request setUseCount:useCount;
	[request setCallback:^ (GSBuyVirtualGoodResponse* response) {
	NSArray* boughtItems = [response getBoughtItems]; 
	NSNumber* currency1Added = [response getCurrency1Added]; 
	NSNumber* currency2Added = [response getCurrency2Added]; 
	NSNumber* currency3Added = [response getCurrency3Added]; 
	NSNumber* currency4Added = [response getCurrency4Added]; 
	NSNumber* currency5Added = [response getCurrency5Added]; 
	NSNumber* currency6Added = [response getCurrency6Added]; 
	NSNumber* currencyConsumed = [response getCurrencyConsumed]; 
	NSNumber* currencyType = [response getCurrencyType]; 
	NSDictionary* scriptData = [response getScriptData]; 
	NSArray* transactionIds = [response getTransactionIds]; 
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
	
	void PsnBuyGoodsRequest_Response(GS& gsInstance, const BuyVirtualGoodResponse& response) {
	gsstl:vector<Types::Boughtitem*> boughtItems = response.getBoughtItems(); 
	Optional::t_LongOptional currency1Added = response.getCurrency1Added(); 
	Optional::t_LongOptional currency2Added = response.getCurrency2Added(); 
	Optional::t_LongOptional currency3Added = response.getCurrency3Added(); 
	Optional::t_LongOptional currency4Added = response.getCurrency4Added(); 
	Optional::t_LongOptional currency5Added = response.getCurrency5Added(); 
	Optional::t_LongOptional currency6Added = response.getCurrency6Added(); 
	Optional::t_LongOptional currencyConsumed = response.getCurrencyConsumed(); 
	Optional::t_LongOptional currencyType = response.getCurrencyType(); 
	GSData scriptData = response.getScriptData(); 
	gsstl:vector<gsstl::string> transactionIds = response.getTransactionIds(); 
	}
	......
	
	PsnBuyGoodsRequest request(gsInstance);
	request.SetAnalyticsData(analyticsData)
	request.SetAuthorizationCode(authorizationCode)
	request.SetEntitlementLabel(entitlementLabel)
	request.SetRedirectUri(redirectUri)
	request.SetUniqueTransactionByPlayer(uniqueTransactionByPlayer)
	request.SetUseCount(useCount)
	request.Send(PsnBuyGoodsRequest_Response);
```

### Java
```java
import com.gamesparks.sdk.api.autogen.GSRequestBuilder.PsnBuyGoodsRequest;
import com.gamesparks.sdk.api.autogen.GSResponseBuilder.BuyVirtualGoodResponse;
import com.gamesparks.sdk.api.autogen.GSTypes.*;
import com.gamesparks.sdk.api.GSEventListener;

...
gs.getRequestBuilder().createPsnBuyGoodsRequest()
	.setAnalyticsData(analyticsData)
	.setAuthorizationCode(authorizationCode)
	.setEntitlementLabel(entitlementLabel)
	.setRedirectUri(redirectUri)
	.setUniqueTransactionByPlayer(uniqueTransactionByPlayer)
	.setUseCount(useCount)
	.send(new GSEventListener<BuyVirtualGoodResponse>() {
		@Override
		public void onEvent(BuyVirtualGoodResponse response) {
			List<Boughtitem> boughtItems = response.getBoughtItems(); 
			Long currency1Added = response.getCurrency1Added(); 
			Long currency2Added = response.getCurrency2Added(); 
			Long currency3Added = response.getCurrency3Added(); 
			Long currency4Added = response.getCurrency4Added(); 
			Long currency5Added = response.getCurrency5Added(); 
			Long currency6Added = response.getCurrency6Added(); 
			Long currencyConsumed = response.getCurrencyConsumed(); 
			Integer currencyType = response.getCurrencyType(); 
			GSData scriptData = response.getScriptData(); 
			List<String> transactionIds = response.getTransactionIds(); 
		}
	});

```

### Cloud Code
```javascript

	var request = new SparkRequests.PsnBuyGoodsRequest();
	request.analyticsData = ...;
	request.authorizationCode = ...;
	request.entitlementLabel = ...;
	request.redirectUri = ...;
	request.uniqueTransactionByPlayer = ...;
	request.useCount = ...;
	var response = request.Send();
	
var boughtItems = response.boughtItems; 
var currency1Added = response.currency1Added; 
var currency2Added = response.currency2Added; 
var currency3Added = response.currency3Added; 
var currency4Added = response.currency4Added; 
var currency5Added = response.currency5Added; 
var currency6Added = response.currency6Added; 
var currencyConsumed = response.currencyConsumed; 
var currencyType = response.currencyType; 
var scriptData = response.scriptData; 
var transactionIds = response.transactionIds; 
```


