---
nav_sort: 3
src: /Tutorials/Game Engine Integrations/Unreal CPP Leaderboard Entries.md
---

# Accessing Leaderboard Entries in Unreal CPP

This tutorial shows you how to extract and print Leaderboard entries in Unreal CPP using a [LeaderboardDataRequest](/API Documentation/Request API/Leaderboards/LeaderboardDataRequest.md). To do this, we'll build two functions to handle the request and the response. These functions will be in your class's CPP file, so make sure you declare these functions in your header file.

<q>**General Method!** The following example of how to work with Leaderboard data demonstrates an approach that you can use as a general method for extracting Leaderboard data entries.</q>

## Building the Request

```

void AMyClass::function()
{
//GS Instance reference
GameSparks::Core::GS& gs = UGameSparksModule::GetModulePtr()->GetGSInstance();
//Create request instance
GameSparks::Api::Requests::LeaderboardDataRequest leaderboardRequestInstance(gs);
//Set Shortcode
leaderboardRequestInstance.SetLeaderboardShortCode("High_Score_Leaderboard");
//Set max entry count (max entries returned)
leaderboardRequestInstance.SetEntryCount(50);
//Send request and reference response listener function
leaderboardRequestInstance.Send(LeaderboardData_Response);
}

```

## Building the Response

```

void AMyClass::LeaderboardData_Response(GameSparks::Core::GS&, const GameSparks::Api::Responses::LeaderboardDataResponse& response)
{
	//Check if response is error free
	if (!response.GetHasErrors()) {
		//For every entry returned in Data object (Entries object)
		for (int i = 0; i < response.GetData().size(); i++) {
			//SCORE is the ShortCode for the event attribute linked to this Leaderboard, this will be unique to your event
			FFloat16 score = response.GetData()[i].GetBaseData().GetFloat("SCORE").GetValue();
			//Get player name
			std::string playerName = response.GetData()[i].GetUserNameW().GetValue();
			//Get rank in Leaderboard
			int rank = response.GetData()[i].GetRank().GetValue();
			//Print results
			GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Blue, FString::FromInt(rank) + FString(" ") + playerName.c_str() + FString(" ") + FString::SanitizeFloat(score));
		}
	}

}

```

<q>**Getting the Data Values!** Here the main thing to note is that we use *GetData* in the response to get an array of entries and each index of the array references an object. We then then use *GetBaseData* to get the values within the object.</q>

Other Leaderboard entry requests will behave similarly. This example demonstrates the basic sequence for extracting entries from any Leaderboard request.
