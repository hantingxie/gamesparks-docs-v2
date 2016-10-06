---
nav_sort: 5
src: /Tutorials/Game Engine Integrations/Using the SetDurable Parameter.md
---

# SetDurable

SetDurable is a function parameter in the Unity version of the GameSparks SDK. When you send a Request with *.SetDurable(true)* it will store your request in a queue to be sent to GameSparks in the event of your device being disconnected from the network.

This functionality enables your game to withstand random disconnects from the internet and allow a highscore to be posted after it was achieved, or a challenge turn to be taken and sent to GameSparks, once the connection has been restored.

For instance, a player is using a cellular connection on a train to play Tic Tac Toe. The player has already loaded our game, cached the latest instances of our challenges and friends. The train then enters a tunnel and the player loses their connection. Normally in this sort of case, if the player went to challenge a friend and take a turn, or tried to take a turn on the already running game without the connection, they'd receive an error and Tic Tac Toe should inform them that it has lost it's connection.

However, with SetDurable, the player can still challenge a friend, and set their first turn, load a cached instance of a challenge and also take their turn. Then when the train emerges from the tunnel and the player's connection is restored, the game sends these requests in the same order they were submitted.

## Examples

### Logging a new score in the Leaderboard

```
    new GameSparks.Api.Requests.LogEventRequest_postScore()
    	.Set_score(scoreToBePassed)
    	.SetDurable(true)
    	.Send((response) =>
    {
            if (response.HasErrors)
            {
                    Debug.Log("Failed");
            }
            else
            {
                    Debug.Log("New Score of "+ scoreToBePassed +" Posted Successful");
            }
    });
```

### Taking a turn in a challenge

```    
    new LogChallengeEventRequest().SetChallengeInstanceId(challengeInstanceId)
    	.SetEventKey("takeTurn")
    	.SetEventAttribute("pos", pos)
    	.SetEventAttribute("playerIcon", playerIcon)
    	.SetDurable(true)
    	.Send((response) =>
    {
            if (response.HasErrors)
            {

            }
            else
            {
                    // If our ChallengeEventRequest was successful we inform the player
                    sent.PlayForward();
            }
    });

```
