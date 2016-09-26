---
nav_sort: 3
src: /Tutorials/Social Authentication and Player Profile/Automating User Password Change.md

---

# User Password Change


## Introduction

If one of your users loses or forgets their password, you'll want an automated way for them to retrieve it.

This tutorial shows you how to set up Cloud Code to do this. The set up described here is the most basic way users have access to your platform without them having to be authenticated and can be developed for more advanced and specific applications.    

## Cloud Code Section

### Choosing our sequence of actions and passing in scriptData

*1.* Navigate to the *Configurator* > *Cloud Code*.

*2.* Select [AuthenticationRequest](/API Documentation/Request API/Authentication/AuthenticationRequest.md) under *Bindings* > *Requests*. The *Cloud Code* editor opens for the request and you can start editing it. This will allow users to run the password recovery logic without having an authenticated account.
* **Action.** The first thing the *Cloud Code* will need to work is the '*action*' variable. The '*action*' variable will determine which sequence of instructions to perform. In this example, we have two sequences - password recovery and password reset:
  * Password recovery will generate a token which will be sent via email.
  * Password reset will take this token and a password and change the password.
* **Status.** The '*status*' variable will help you debug and determine whether the function was successfully completed and, if not, will help you print out why not.

```    
    	var status = "Started";

    if(Spark.data.scriptData){ //Checking if there is any scriptData passed in, if not then carry on the authentication as normal

        var action = Spark.data.scriptData.action;

        if("passwordRecoveryRequest" === action){
            startRecovery(Spark.data.scriptData); //Start recovery sequence

        } else if ("resetPassword" === action){
            resetPassword(Spark.data.scriptData); //Start reset sequence
        }

        else
        {
            status = "invalid action"; // action variable isn't valid, check spelling or value
        }

        Spark.setScriptError("action", status); // set an error to prevent the AuthenticationRequest being processed

    }
```  

### Password Recovery Sequence

*4.* Next, you'll need to link the user account to an E-mail. You can do this:
* Through the initial authentication using *scriptData*.
* Later on through an event by saving it on the player using *setScriptData*.

If the email passed in is linked to an account, then:
* A unique token will be generated linked to the account.
* The email sending function will be called, which sends an email containing the token to be used in the reset password sequence to change the password.

```  
    function startRecovery(request){
        if(!request.email){
            status = "email variable not passed in"; //Either email variable was not passed in pr spelt incorrect
            return;
        }
        var players = Spark.systemCollection("player");
        var playerId = players.findOne({"scriptData.email" : request.email}, {_id : 1, displayName:1}); // requires an 'email' value to be set on each player via setScriptData, and an index to exist on scriptData.email
        if(!playerId){
            status = "invalid"; //Email is incorrect or account isn't linked to one
            return;
        }
        var token = generateRecoveryToken(); // Function to generate a unique token
        var player = Spark.loadPlayer(playerId._id.$oid);
        player.setScriptData("passwordRecoveryToken", token); //Sends the token back with the response
        sendRecoveryEmail(request.email, playerId.displayName, token); // Function used to send email
        status = "complete"; // Successfully found player and attempted to send email
    }
```  	


### Token Generation

*5.* This is our example of a token generating function. Yours could be anything you want it to be, but be careful that there aren't any duplicates because that would cause you a lot of problems. This is a simple string, which retrieves the date combined with *randomlyGeneratedToken-*, which can easily be taken advantage of.


    	function generateRecoveryToken(){
        return "randomlyGeneratedToken-" + new Date().getTime();} // this should be cryptographically strong, not simply date-based


### Sending out the E-Mail

*6.* We have full integration with *SendGrid* services. If you plan to use it to send your E-Mails, then create an account with them and wait for their E-Mail confirming that: *"Your SendGrid account has been provisioned!"*, which then allows you to start sending emails. It might take up to 24 hours to receive it. You'll need:
* The E-Mail to send to.
* The E-Mail sent from.
* The E-mail Subject.
* The E-Mail contents.
* To send the E-Mail.

```    
    	function sendRecoveryEmail(email, name , token){

        var myGrid = Spark.sendGrid("Username", "Password"); //Here we use sendGrid as an example because we have full integration with their services.

        myGrid.addTo( email , name ); //The email to send the message to and the name of the user

        myGrid.setFrom("Email", "Name"); //Here you'd leave your organization or personal email

        myGrid.setSubject("Subject"); //The subject of your email

        myGrid.setText(token); // The body and message of your email, here we just send the token

        myGrid.send(); //Finally send the email
    }
```    

### Password Reset Sequence

*7.* Finally, you have the password reset function, which takes a token and password parameter and checks to see if the Token is linked to an account. If it is, then it sets the password of that account to the new password passed in.

```    
    	function resetPassword(request){
        if(!request.token || !request.password){
            status = "Password or token variable not passed in";  //Either bad spelling or no variables passed in
            return;
        }
        var players = Spark.systemCollection("player");
        var playerId = players.findOne({"scriptData.passwordRecoveryToken" : request.token}, {_id : 1}); // requires an index to exist on scriptData.passwordRecoveryToken
        if(!playerId){
            status = "invalid"; //Token incorrect, bad spelling or Token used already
            return;
        }
        var player = Spark.loadPlayer(playerId._id.$oid);
        player.setScriptData("passwordRecoveryToken", null); // make sure the token can only be used once
        var changePasswordRequest = new SparkRequests.ChangeUserDetailsRequest();
        changePasswordRequest.newPassword = request.password;
        changePasswordRequest.SendAs(player.getPlayerId());// Simulate player changing their details using ChangeUserDetailsRequest
        status = "complete"; // Successfully changed password
    }
```

## Changing Password Using The SDK


### Sending E-Mail

*8.* For this step you'll have to allow the user to input their E-Mail:
* When they've passed in their E-Mail, you'll need to have a function which creates an *object* (New Object, GSData, GSRequestData) which stores the '*email*' and '*action*' variables.
* The '*action*' string variable will be set to "*passwordRecoveryRequest*".
* When both variables have been set and stored in the object, call the *AuthenticationRequest* and send that object as *scriptData*. Make sure you leave spaces or quotes for both Username and Password fields for the *AuthenticationRequest*.


### Changing Password

*9.* After the player has been sent a token, they'll want to be able to change their password:
* Allow the player to input their token and a new password.
* When the player has passed these values through, create an object which stores the variable '*token*' as a string, '*password*' as a string which will store the value of the password passed in and '*action*' as a string set as "*resetpassword*".
* When the object has been set, send it as *scriptData* using the *AuthenticationRequest*. Make sure you leave spaces or quotes for both Username and Password fields for the *AuthenticationRequest*.
