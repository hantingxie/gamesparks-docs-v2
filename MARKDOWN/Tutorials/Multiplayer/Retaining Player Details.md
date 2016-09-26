---
nav_sort: 2
src: /Tutorials/Multiplayer/Retaining Player Details.md
---

# Retaining Player Details

## Introduction

Once you match players together you will have reference to other player's Ids and account variables to use in Cloud code. One of the things you can do is easy access of player data. This will enable you to load player specific options, settings and personal data the moment the match is made.  

## Accessing Player Data

To access player data from a list of opponents in a match:

  * Call the MatchDetails request using the matchId of the match which contains the players you wish to access.
  * Once you receive the response, you can access the opponent array which contains player data object. This gives you easy access to Achievements, Virtual Goods, Display name, online status, ID and scriptData, so you don't have to load player information through ID but instead have a quick reference to commonly used data.
 

  ```  
    {
     "@class": ".MatchDetailsResponse",
     "matchId": "565dc32ce4b0905d7600a5a0",
     "opponents": [
      {
       "achievements": [
        "Cloud_Achievement",
        "Fastest_First"
       ],
       "online": true,
       "id": "563b423ce4b0f85acff00a61",
       "displayName": "Dummy2"
      },
      {
       "achievements": [
        "Cloud_Achievement"
       ],
       "online": false,
       "id": "563b4243e4b0f85acff00a69",
       "displayName": "Dummy3"
      },
      {
       "achievements": [
        "Cloud_Achievement"
       ],
       "online": false,
       "id": "563b4249e4b0f85acff00a71",
       "displayName": "Dummy4"
      }
     ],
     "playerId": "563b4235e4b0f85acff00a22",
     "scriptData": null
    }
```
