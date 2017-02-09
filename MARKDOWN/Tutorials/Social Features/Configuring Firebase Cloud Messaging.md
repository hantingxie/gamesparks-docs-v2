---
nav_sort: 2
src: /Tutorials/Social Features/Configuring Firebase Cloud Messaging.md
---

# How to Configure Google Firebase Cloud Messaging service

Google allows push notifications through its Firebase Cloud Messaging (FCM) service. FCM is a multi-platform service available on Android, iOS, and Web based applications.

In this tutorial, you'll learn how to set up your application with FCM, enable push notifications, and get your GameSparks game set up to allow it to send notifications to your players on your behalf.

## Creating an Application on Firebase

Firstly, you need to set up an application with [Firebase](https://console.firebase.google.com/):
* Click *CREATE NEW PROJECT*:

![](img/FirebaseCM/1.png)

On the *Create a project* dialog, give your project a name and a region, then click *CREATE PROJECT*:

![](img/FirebaseCM/2.png)

## Finding your FCM Server Key  

Once your app has been created:

*1.* Click The *Settings* button - the cog icon under your project name - and then click *Project Settings*.

![](img/FirebaseCM/3.png)

*2.* Click the *Cloud Messaging* tab and you'll see your *Server key* under *Project Credentials*:

![](img/FirebaseCM/4.png)


## Configuring your GameSparks Game

Now that you have the Firebase *Server key*, the next step is to configure your GameSparks game so that you can send push notifications.

*1.* Navigate to *Configurator > Integrations*:

![](img/FirebaseCM/5.png)

*2.* Select *Google* (Your game must have Google integration enabled):

![](img/FirebaseCM/6.png)

*3.* Click *Edit*.

*4.* Scroll down to *FCM Server Key* field.

*5.* Enter the Server key from the Firebase Console into the *FCM Server Key* field:

![](img/FirebaseCM/7.png)

*6.* Click *Save*.

That's all there is to it! Your GameSparks game is now configured to send push notifications to your players on your behalf.

## Implementing FCM on your application

Full details of the FCM implementation is beyond the scope of this tutorial, but there are excellent resources available to help you get going with this. The [official Firebase documentation](https://firebase.google.com/docs/cloud-messaging) is a great place to start and covers registering your player's device with FCM depending on your platform.


## Registering a Device for Push Notifications

The final step required to actually deliver a push notification is for the GameSparks service to be able to identify your player's device and thus be able to send the notifications. This is accomplished with a [PushRegistrationRequest](/API Documentation/Request API/Misc/PushRegistrationRequest.md).

For an authenticated player in the GameSparks Test Harness, send:

```
{ "@class": ".PushRegistrationRequest",
"deviceOS": "fcm",
"pushId": "DEVICE_REGISTRATION_ID",
"requestId": "1399640846121" }

```

Where *DEVICE_REGISTRATION_ID* is the registration id returned from the call to:

| Platform/Language  | Call  |
|---|---|
| Android  |  FirebaseInstanceID.getToken() |
| iOS/OC  | NSString *refreshedToken = [[FIRInstanceID instanceID] token];  |
| iOS/Swift  | let token = FIRInstanceID.instanceID().token()!  |
| Web  | firebase.messaging()  |

The GameSparks platform is now capable of pushing messages to this player, even while they're not actually playing your game.

For more details on push notifications within the GameSparks platform, check out [Messaging](/Documentation/Key Concepts/Messaging.md).
