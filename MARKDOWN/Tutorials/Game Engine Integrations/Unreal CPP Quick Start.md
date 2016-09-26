---
nav_sort: 2
src: /Tutorials/Game Engine Integrations/Unreal CPP Quick Start.md
---

# Unreal CPP QuickStart

## Initialization

To integrate the GameSparks platform into your C++ project, perform the following two initialization stages:
* GameMode Header
* Gamemode Body


### GameMode.h

*1.* Include the following headers:

```
#include "GameSparks/Private/GameSparksComponent.h"
#include <GameSparks/GS.h>
#include <GameSparks/generated/GSResponses.h>
#include "GameSparks/Private/GameSparksModule.h"
#include <GameSparks/generated/GSRequests.h>

```

*2.* Create a variable for the GameSparks component:

```

UGameSparksComponent* GameSparksComp;

```

*3.* Add your GameMode's constructor and begin play. With it a UFUNCTION with a bool parameter to handle the *OnGameSparksAvailableDelegate* invocation:

```

//Constructor
	AMyGameMode();

	//BeginPlay
	virtual void BeginPlay() override;

	//Function used to determine what happens if GameSparks connects or fails to (Needs to be UFUNCTION)
	UFUNCTION()
	void OnGameSparksAvailable(bool available);

```

### GameMode.CPP

*1.* In your GameMode's constructor initialize the GameSparks Component:

```

AMyGameMode::AMyGameMode() {

	//Initialize GameSparksComponent used to connect
	GameSparksComp = CreateDefaultSubobject<UGameSparksComponent>(TEXT("GSparkComp"));

}

```

*2.* In your GameMode's BeginPlay function add your handler function to the *OnGameSparksAvailableDelegate* invocation list then call the Connect function from your GameSparks Component:

```

void AMyGameMode::BeginPlay() {

	Super::BeginPlay();
	//Add a function to the OnGameSparksAvailableDelegate invocation list
	GameSparksComp->OnGameSparksAvailableDelegate.AddDynamic(this, &AMyGameMode::OnGameSparksAvailable);
	//Connect to GameSparks using Key and Secret
	GameSparksComp->Connect("293711ZXWjA9", "DgnYnPUE2D0RetwKAy5XPUxxxN7pl36e");

}

```

*3.* Finally just add logic to your handler function to execute code when GameSparks becomes available:

```

//OnAvailable Handler
void AMyGameMode::OnGameSparksAvailable(bool available) {

		if (available) {
		GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Red, TEXT("Connected"));
		//Get a pointer to the module's GSInstance
		GameSparks::Core::GS& gs = UGameSparksModule::GetModulePtr()->GetGSInstance();

		//Construct an Authentication request
		GameSparks::Api::Requests::AuthenticationRequest authRequest(gs);
		authRequest.SetUserName("gstest");
		authRequest.SetPassword("pass");
		authRequest.SetUserData(this);
		//Send it with a pointer to the function that will handle the response
		authRequest.Send(AuthenticationRequest_Response);
	}
}

//Example response function
void AMyGameMode::AuthenticationRequest_Response(GameSparks::Core::GS&, const GameSparks::Api::Responses::AuthenticationResponse& response)
{
	GEngine->AddOnScreenDebugMessage(-1, 20.f, FColor::Red, response.GetJSONString().c_str());
	//Check is response has no errors
	if (!response.GetHasErrors()) {
		GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Red, TEXT("Auth response successful"));

		GameSparks::Core::GS& gs = UGameSparksModule::GetModulePtr()->GetGSInstance();
		GameSparks::Api::Requests::AccountDetailsRequest accDetRequest(gs);
		//If no errors then send an accounts details request
		accDetRequest.Send(AccountDetailsRequest_Response);

	}
}

```

<Q>**C++ GameSparks Functions!** Refer to the [CPP quick start guide](/Tutorials/Game Engine Integrations/CPP Quick Start.md) for simple C++ GameSparks functions.</q>
