---
nav_sort: 3
src: /Tutorials/Social Authentication and Player Profile/Automating User Password Change.md

---

# User Password Change

## Introduction

If one of your users loses or forgets their password, you'll want an automated way for them to retrieve it.

This tutorial shows you how to set up Cloud Code to do this. The set up described here is the most basic way users have access to your platform without them having to be authenticated and can be developed for more advanced and specific applications.    

## Cloud Code Section

### Choosing Our Sequence of Actions and Passing in scriptData

*1.* Navigate to the *Configurator* > *Cloud Code*.

*2.* Under *Scripts* click to expand the *Requests* area and then select [AuthenticationRequest](/API Documentation/Request API/Authentication/AuthenticationRequest.md). The *Cloud Code* editor opens for the request and you can start editing it. This will allow users to run the password recovery logic without having an authenticated account.
* **Action.** The first thing the *Cloud Code* will need to work is the *'action'* variable. The *'action'* variable will determine which sequence of instructions to perform. In this example, we have two sequences - password recovery and password reset:
  * Password recovery will generate a token which will be sent via email.
  * Password reset will take this token and a password and change the password.
* **Status.** The *'status'* variable will help you debug and determine whether the function was successfully completed and, if not, will help you print out why not.

```    
var status = "Started";
//Checking if there is any scriptData passed in, if not then carry on the authentication as normal
if(Spark.data.scriptData){

    var action = Spark.data.scriptData.action;

    if("passwordRecoveryRequest" === action){
        //Start recovery sequence
        startRecovery(Spark.data.scriptData);

    } else if ("resetPassword" === action){
        //Start reset sequence
        resetPassword(Spark.data.scriptData);
    }

    else
    {
        // action variable isn't valid, check spelling or value
        status = "invalid action";
    }
// set an error to prevent the AuthenticationRequest being processed
    Spark.setScriptError("action", status);

}

```  

### Password Recovery Sequence

Next, you'll need to link the user account to an E-mail. You can do this:

* Through the initial registration using *scriptData*. Use this code in the registration request and response to save the email.
* Later on through an Event by saving it on the player using *setScriptData*.

If the email passed in is linked to an account, then:
* A unique token will be generated linked to the account.
* The email sending function will be called, which sends an email containing the token to be used in the reset password sequence to change the password.

Below is an example of how to save Emails on users and keep track of them so you can generate and send users tokens change their passwords with. For this to work you need a runtime collection to save emails and tokens in with the player's unique ID for easy reference. Our collection used in this example is named "playerEmailCollection":

*The Request Cloud Code:*
```
//Check if scriptData has been passed in to avoid errors
if(Spark.getData().scriptData !== null){
    //Check if the email has been passed in to avoid errors
    if(Spark.getData().scriptData.email === null){
        //If no email has been passed in, force an error to make sure player is not registered
        Spark.setScriptError("error", "DEFINE EMAIL");
    }else{
        //If email is passed in, set it as scriptData so that the response can access it
        //Load email collection
        var emailCollection = Spark.runtimeCollection("playerEmailCollection");
        //Load Email passed in
        var email = Spark.getData().scriptData.email;
        //Compare that email to the database and deny registration if email is already in use
        var checkEmail = emailCollection.findOne({"email":email});
        if(checkEmail === null){
            Spark.setScriptData("email", email)
        } else{
            Spark.setScriptError("error", "EMAIL TAKEN")
        }
    }
}  else{
    //If no scriptData has been passed in, set an error and output useful message
    Spark.setScriptError("error", "DEFINE EMAIL");    
}
```

*The Response Cloud Code:*
```
//Check if player attempting to register isn't already registered
if(Spark.getData().newPlayer === true){
    //If no script errors from request then run sequence
    if(!Spark.hasScriptErrors()){
        //Load email
        var email = Spark.getData().scriptData.email;
        //Set the email as scriptData to keep track of it
        Spark.getPlayer().setScriptData("email", email);
        //Or set the email as privateData to keep track of it
        Spark.getPlayer().setPrivateData("email", email);
        //Load email collection
        var emailCollection = Spark.runtimeCollection("playerEmailCollection");

        //Save the email on the email collection using the players ID as the document's ID for easy reference later on.
        emailCollection.insert({"_id":{"$oid":Spark.getPlayer().getPlayerId()},"email":email});
    }
}
```

*Sending the Request:*
```
{
  "@class": ".RegistrationRequest",
  "displayName": "testUser",
  "password": "password",
  "userName": "testUser",
  "scriptData":{"email":"test@test.com"}
}
```

Below is an example code of how to create a system that saves emails and generates token for password recovery:

### Sequence picker

Depending on the 'action' scriptData input, we're going to decide the sequence the script is going to follow.

```
var status = "Started";
//Checking if there is any scriptData passed in and if not, then carry on the authentication as normal
if(Spark.data.scriptData){

    var action = Spark.data.scriptData.action;

    if("passwordRecoveryRequest" === action){
        //Start recovery sequence
        startRecovery(Spark.data.scriptData);

    } else if ("resetPassword" === action){
        //Start reset sequence
        resetPassword(Spark.data.scriptData);
    }

    else
    {
        // action variable isn't valid, check spelling or value
        status = "invalid action";
    }
// set an error to prevent the AuthenticationRequest being processed
    Spark.setScriptError("action", status);

}
```

### Token Generation

This is our example of a token generating function. Yours could be anything you want it to be, but be careful that there aren't any duplicates because that would cause you a lot of problems. This is a simple string, which retrieves the date combined with *randomlyGeneratedToken-*, which can easily be taken advantage of.

```
function generateRecoveryToken(){
    // this should be cryptographically strong, not simply date-based
    return "randomlyGeneratedToken-" + new Date().getTime();
}
```

### Sending out the E-Mail

We have full integration with *SendGrid* services. If you plan to use it to send your E-Mails, then create an account with them and wait for their E-Mail confirming that: *"Your SendGrid account has been provisioned!"*, which then allows you to start sending emails. It might take up to 24 hours to receive it. You'll need:

* The E-Mail to send to.
* The E-Mail sent from.
* The E-mail Subject.
* The E-Mail contents.
* To send the E-Mail.

```    
function sendRecoveryEmail(email, name , token){
    //Here we use sendGrid as an example because we have full integration with their services.
    var myGrid = Spark.sendGrid("Username", "Password");
    //The email to send the message to and the name of the user
    myGrid.addTo( email , name );
    //Here you'd leave your organization or personal email
    myGrid.setFrom("Email", "Name");
    //The subject of your email
    myGrid.setSubject("Subject");
    // The body and message of your email, here we just send the token
    myGrid.setText(token);
    //Finally send the email
    myGrid.send();
}
```    

If you don't want to use *sendGrid* you can use [SparkHTTP](/API Documentation/Cloud Code API/Integrations/SparkHttp.md) to use your own provider.

### Password Recovery Sequence

The password recovery sequence is going to generate a token, save it on the player's email collection, and send the player an email with a token.

```  
function startRecovery(request){
    if(!request.email){
        //Either the email variable was not passed in or it was spelt incorrectly
        status = "email variable not passed in";
        return;
    }
    var emailsCollection = Spark.runtimeCollection("playerEmailCollection")
    // requires an 'email' value to be set on each player via setScriptData, and an index to exist on scriptData.email
    var playerId = emailsCollection.findOne({"email" : request.email}, {_id : 1, displayName:1});
    if(playerId === null){
        //Email is incorrect or account isn't linked to one
        status = "invalid";
        return;
    }
    // Function to generate a unique token
    var token = generateRecoveryToken();
    var player = Spark.loadPlayer(playerId._id.$oid);
    Spark.setScriptData("token", token)
     //Sends the token back with the response
     emailsCollection.update({"_id":{"$oid":playerId._id.$oid}}, {$set: {"token":token}});
    player.setScriptData("passwordRecoveryToken", token);
   // Function used to send email
    sendRecoveryEmail(request.email, playerId.displayName, token);
    // Successfully found player and attempted to send email
    status = "complete";
}
```  	

### Password Reset Sequence

Finally, you have the password reset function, which takes a token and password parameter and checks to see if the Token is linked to an account. If it is, then it sets the password of that account to the new password passed in.

```    
function resetPassword(request){
  if(!request.token || !request.password){
      //Either bad spelling or no variables passed in
      status = "Password or token variable not passed in";  
      return;
  }
  var emailsCollection = Spark.runtimeCollection("playerEmailCollection");
  // requires an index to exist on scriptData.passwordRecoveryToken
  var playerId = emailsCollection.findOne({"token" : request.token}, {_id : 1});
  if(!playerId){
      //Token incorrect, bad spelling, or Token used already
      status = "invalid";
      return;
  }
  var player = Spark.loadPlayer(playerId._id.$oid)
  // make sure the token can only be used once by updating the player's email document token to null
  emailsCollection.update({"_id":{"$oid":playerId._id.$oid}}, {$set: {"token":""}})
  //Create a change user details request
  var changePasswordRequest = new SparkRequests.ChangeUserDetailsRequest();
  //Pass in the new password
  changePasswordRequest.newPassword = request.password;
  // Simulate player changing their details using ChangeUserDetailsRequest
  changePasswordRequest.SendAs(player.getPlayerId());
  // Successfully changed password
  status = "complete";
}
```

## Changing Password Using The SDK


### Sending E-Mail

For this step you'll have to allow the user to input their e-mail:
* When they've passed in their e-mail, you'll need to have a function which creates an *object* (New Object, GSData, GSRequestData) which stores the *'email'* and *'action'* variables.
* The *'action'* string variable will be set to *"passwordRecoveryRequest"*.
* When both variables have been set and stored in the object, call the *AuthenticationRequest* and send that object as *scriptData*. Make sure you leave spaces or quotes for both Username and Password fields for the *AuthenticationRequest*.


### Changing Password

After the player has been sent a token, they'll want to be able to change their password:
* Allow the player to input their token and a new password.
* When the player has passed these values through, create an object which stores the variable '*token*' as a string, *'password'* as a string which will store the value of the password passed in and *'action'* as a string set as *"resetpassword"*.
* When the object has been set, send it as *scriptData* using the *AuthenticationRequest*. Make sure you leave spaces or quotes for both Username and Password fields for the *AuthenticationRequest*.
