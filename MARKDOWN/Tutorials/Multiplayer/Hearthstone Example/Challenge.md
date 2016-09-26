---
nav_sort: 3
src: /Tutorials/Multiplayer/Hearthstone Example/Challenge.md
---

# Challenge

This section will heavily rely on Challenge events, there will be a lot of calls to retrieve and save the cards, stats, playingField and currentHand. Player Ids and Challenge Id will constantly be values to reference the rest of the game, these two Ids will allow you to do anything with the challenge. Create 4 events:

* action_pullCard
* action_pushCard
* action_playCard
* action_endTurn

<q>**Important!** Make sure the cloud code for these events cloud code is edited in the challenge event tab of the cloud code section *not the event's tab*.</q>

## action_pullCard

When calling challenge events you'll automatically get a challengeInstanceId string input value.

This challenge event relies on the pullCard module. It adds a random card from the deck into the player's current hand. The player is unable to pull another card from the deck during this round after this event is executed.

```
  //Load challenge
  var chal = Spark.getChallenge(Spark.getData().challengeInstanceId);

  //Retrieve player stats
  var playerStats = chal.getScriptData("playerStats");
  //Retrieve player Id
  var pId = Spark.getPlayer().getPlayerId();

  if(playerStats[pId].hasPulled === false){

      //Retrieve current hands
      var currentHand = chal.getScriptData("currentHand");

      //Run the sequence to pull a new card
      require("pullCardModule");

      //Player can't pull another card this round
      playerStats[pId].hasPulled = true;

      //Save current hand and player stats
      chal.setScriptData("currentHand", currentHand);
      chal.setScriptData("playerStats", playerStats);
  }
  else{
      Spark.setScriptError("Error", "Already pulled card this round");
  }
```

## action_pushCard

This event will have 2 input values:
* challengeInstanceId - To input the challenge's Id
* slotNum which is the name of the card (example c0,c1).

This event will move cards from the currentHand to the playField if the player has enough mana to play the card. Using the unqiue Id given to the card (for example c1 or c0) we move the card from one object to another. If cards have certain effects such as charge or direct attack that will trigger a sequence of code.

```
  //Load the challenge
  var chal = Spark.getChallenge(Spark.getData().challengeInstanceId);
  //Retrieve player Id
  var pId = Spark.getPlayer().getPlayerId();

  //Retrieve the slot
  var cardName = Spark.getData().slotNum;
  //Retrieve the current hand
  var currentHand = chal.getScriptData("currentHand");
  //Retrieve the current player's hand
  var playerHand = currentHand[pId];
  //Get the cards name or type
  var cardObj = playerHand[cardName];

  //Retrieve player stats
  var playerStats = chal.getScriptData("playerStats");

  //Retrieve Mana
  var playerMana = playerStats[pId].currentMana;

  //Is there enough mana to spawn the card?
  if( playerMana >= cardObj.spawnCost){

      var playerStats = chal.getScriptData("playerStats");
      //New mana
      playerStats[pId].currentMana = playerStats[pId].currentMana - cardObj.spawnCost;

      //Retrieve the playing field
      var playField = chal.getScriptData("playField");

      if(cardObj.effect === "Charge"){
          //Set value in the correct position (playField -> Players ID -> The card's name/number) with correct name
          playField[pId][cardName] = {"type" : cardObj.type, "atk" : cardObj.atk, "hp" : cardObj.hp, "maxHP": cardObj.hp, "effect": cardObj.effect, "canAtk": true } ;
      }
      else{
          //Set value in the correct position (playField -> Players ID -> The card's name/number) with correct name
          playField[pId][cardName] = {"type" : cardObj.type, "atk" : cardObj.atk, "hp" : cardObj.hp, "maxHP": cardObj.hp, "effect": cardObj.effect, "canAtk": false } ;
      }
      if(cardObj.effect === "Direct Attack"){
          //Determine enemy Id
          if(Spark.getPlayer().getPlayerId() === chal.getChallengerId()){
          //If equal to challenger, then Id is challenged[0] Id
          var opponentId = chal.getChallengedPlayerIds()[0];
          }
          else{
          //If not equal to challenger then other player Id is challenger Id
          var opponentId = chal.getChallengerId();
          }
          //Set opponent players' health
          playerStats[opponentId].playerHealth = playerStats[opponentId].playerHealth - cardObj.atk;
      }
      if(cardObj.effect === "Taunt"){
          playerStats[pId].tauntProtection = true;
      }
      //Remove that card from current hand
      delete currentHand[pId][cardName];

      //Return script message with card pushed
      Spark.setScriptData("result", "Card " + cardName + " of type " + cardObj.type + " is on the playing field");

      //Save jsons
      chal.setScriptData("currentHand", currentHand);
      chal.setScriptData("playField", playField);
      chal.setScriptData("playerStats", playerStats);
  }
  else{
      //if there isn't enough mana, send error report through scriptData
      Spark.setScriptData("Error", "Not enough mana");
  }

```

## action_playCard

This event will have 4 input values:
* challengeInstanceId - To input the challenge's Id
* playState - To distinguish between the current action, we configured "attack" and "heal". This means we don't have to have an event for every action but instead take a modular approach.
* name - The player's chosen card (example c0,c1 etc).
* targetName - Could either be the heal target or attack target depending on playState.

Using this event a player can heal a friendly target or attack an enemy opponent or their cards depending on playState and the targetName.

```
  //Load challenge
  var chal = Spark.getChallenge(Spark.getData().challengeInstanceId);

  //Load data
  var playState = Spark.getData().playState;
  var cardName = Spark.getData().name;
  var targetName = Spark.getData().nameTarget;

  //Retrieve player stats
  var playerStats = chal.getScriptData("playerStats");


  //Retrieve player Id
  var pId = Spark.getPlayer().getPlayerId();

  //Determine enemy Id
  if(Spark.getPlayer().getPlayerId() === chal.getChallengerId()){
      //If equal to challenger, then Id is challenged[0] Id
      var opponentId = chal.getChallengedPlayerIds()[0];
  }
  else{
      //If not equal to challenger then other player Id is challenger Id
      var opponentId = chal.getChallengerId();
  }

  //Load playField
  var playField = chal.getScriptData("playField");
  //Load player play field
  var playerField = playField[pId];

  var attackingCard = playerField[cardName];

  if(attackingCard == null){
     Spark.setScriptError("Error", "Attacking card does not exist");
  }

  //Depending on playState of card
  if(playState === "attack"){
      if(attackingCard.canAtk === true){
          //If our target is the opponent, damage opponent
          if(targetName === "opponent"){
              if(playerStats[opponentId].tauntProtection === true){
                  Spark.setScriptError("Error", "There is a taunt card protecting your opponent")
              }
              else{
                  //Retrieve the playerHealth object
                  var health = playerStats[pId].currentHealth;
                  //Lower the opponent health points based on card's attack
                  playerStats[opponentId].currentHealth = playerStats[opponentId].currentHealth - attackingCard.atk;
                  //Save the health stats
                  chal.setScriptData("playerStats", playerStats);

                  Spark.setScriptData("result", cardName + " attacked opponent")
              }
          }
          else{
              //If our target is not an opponent, then we're aiming for another card

              //Retrieve opponent field
              var opponentField = playField[opponentId];
              //Retrieve target card
              var targetCard = opponentField[targetName];

              if(targetCard == null){
              Spark.setScriptError("Error", "Attacking card does not exist");
              }
              //If our attacking card has more attack than the target card hit points, destroy target card and check if
              //card is a taunt card, if it's a taunt card check for other taunt cards, if none are on playing field
              //remove player protection
              if(attackingCard.atk >= targetCard.hp){
                  delete playField[opponentId][targetName];
                  Spark.setScriptData("result", cardName + " destroyed " + targetName);

                  //Check for effect, if Taunt
                  if(targetCard.effect === "Taunt"){
                  if(checkTaunt(Object.keys(playField[opponentId]), playField[opponentId]) !== true){
                      playerStats[opponentId].tauntProtection = false;
                   };   
                  }
              }
              else {
                  //else if our attacking card cannot kill target card with one hit, lower hit points
                  playField[opponentId][targetName].hp = targetCard.hp - attackingCard.atk;
                  Spark.setScriptData("result", cardName + " hurt " + targetName);
              }

              //If our attacking card has less hit points than target card, destroy our card
              if(targetCard.atk >= attackingCard.hp){
                  delete playField[pId][cardName];
                  Spark.setScriptData("result", cardName + " was destroyed by " + targetName);
              }
              else{
                  //Else if our attacking card has more hit points than the target card's attack, then lower hit points
                  playField[pId][cardName].hp = attackingCard.hp - targetCard.atk;  
                  Spark.setScriptData("result", cardName + " was hurt by " + targetName);
              }

              if( playField[pId][cardName] != null){
              //Disallow this card to be able to attack again this round if it still exists
              playField[pId][cardName].canAtk = false;
              }

                  //Save playing field
                 chal.setScriptData("playField", playField);
                 chal.setScriptData("playerStats", playerStats);
              }
          }
  }
  else{
      Spark.setScriptError("Error", "Card cannot attack this round")
  }

  //If instead our playsState was to heal instead of attack, we won't need to load the opponent's playField and just work
  //With this player's playField exclusively
  if(playState === "heal"){
      if(playField[pId][targetCard] != null){
          //If targetCard has less hit points than max allowed
          if(playField[pId][targetCard].hp <= playField[pId][targetCard].maxHP){
              //Heal card by adding hit points
              playField[pId][targetCard].hp = playField[pId][targetCard].hp + 1;
              //Save playField
              chal.setScriptData("playField", playField);
          }
      }
      else{
          Spark.setScriptData("Error", "Can't find target card");
      }

  }

  //Check opponent's play field to see if any taunt cards remain
  function checkTaunt(arr,obj){
      //Loop through the array of keys of the playField object
     for(var i = 0; i < arr.length; i++ ){
         //For every key, access the 'effect' key pair and check if the effect is taunt
          if(obj[arr[i]].effect === "Taunt"){
              //if any taunt effects remain, return true and keep the tauntProtection boolean true
              return true;    
          }
     }
     //If no taunt effects remain, return false to change the tauntProtection boolean
     return false;
  }
```
## action_endTurn

To allow the other player to have a turn, the player's cards to be able to attack, mana to recharge and extra mana gems earned a player needs to end their turn.

This also is a challenge event because it needs to make a reference to the event, so make sure you edit the challenge event cloud code.

```
  //Load challenge
  var chal = Spark.getChallenge(Spark.getData().challengeInstanceId);
  //Retrieve player Id
  var pId = Spark.getPlayer().getPlayerId();

  //Retrieve player's details and play field
  var playerStats = chal.getScriptData("playerStats");
  var playField = chal.getScriptData("playField");

  //If we have less than 10 mana gems
  if(playerStats[pId].overallMana < 10){

      //Add a mana gem
      playerStats[pId].overallMana = playerStats[pId].overallMana + 1;
  }


  //Current mana will be filled again
  playerStats[pId].currentMana = playerStats[pId].overallMana;

  //Get all the cards on the player's play field
  var cards = Object.keys(playField[pId]);
  //Use the allowAtk function on every card
  cards.forEach(allowAtk)

  //Reset card pulled boolean
  playerStats[pId].hasPulled = false;

  //Save JSONs
  chal.setScriptData("playField", playField);
  chal.setScriptData("playerStats", playerStats);

  //Finish player turn
  chal.consumeTurn(pId);

  function allowAtk(obj){
      //Set the canAtk value to true, to allow the card to attack next turn
      playField[pId][obj].canAtk = true;
  }
```
In combination these events and structure can start and end a game the same way Hearthstone works. You can add more cards, more effects and extra functionality easily as this example was built with modularity and expansion in mind. You can test this using the two tabs that have our test harness open. Registering two players and pitting them against each other (both controlled by you).

This concludes the Hearthstone example. You can customize, add, remove and reinvent this system. This is only one way of achieving this kind of game but playing around with our components and further understanding the way they work you can achieve brilliant results.
