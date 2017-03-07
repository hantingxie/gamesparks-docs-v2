---
nav_sort: 5
src: /Tutorials/Database Access and Cloud Storage/Uploading Binary Content from Game.md
---

# How to Upload Binary Content Directly from your Game

You can give your players the ability to upload binary content to be hosted on the GameSparks platform and, from there, shareable with other players. The way to do this is fairly straightforward and you must complete the following steps:
1. Request a URL from the platform to which you can upload the content.
2. Upload the content to the URL provided by the platform.
3. Once content has been uploaded, you'll want the player (or other players) to be able to retrieve the content for use.

In this exercise we'll run through how you complete each of these steps with the GameSparks API and demonstrate this using the [Test Harness](/Documentation/Test Harness/README.md). To finish, there is a brief note on using the GameSparks SDKs to perform these steps (which we've streamlined behind the scenes to make your life easier).

<q>**Upload File Size Limit?** For the file size limit imposed on uploaded content, see [System Limits](/Documentation/Key Concepts/System Limits.md).</q>

## Get an Upload URL

The first step is to get an upload URL - you need somewhere to post your content. If you're following these steps in the Test Harness, the *GetUploadUrlRequest* is available under the *Upload* category (make sure you've authenticated as a player before making the first request).

A [GetUploadUrlRequest](/API Documentation/Request API/Misc/GetUploadUrlRequest.md) made by an authenticated player will result in a response containing a *url* attribute.

<q>**URL Attribute has limited Lifespan!** Upload URLs are one-shot URLs that expire after a matter of minutes so don't hang onto them - if you don't use it right away, throw it away and request another one.</q>

```
{
  "@class": ".GetUploadUrlRequest"
}

```
 

```
{
 "@class": ".GetUploadUrlResponse",
 "url": "https://gsp-aeu000-se04.gamesparks.net/upload/288934CFkBXg/16fc457d-656e-47ea-ad28-00595ec04054/3d3cbd17d2584e8295756d021dd0888b"
}

```


## Upload the Content

Now that you have the upload URL you need to post the file. This is done using a multipart/form-data post - we'd recommend checking it out in the Test Harness because we've provided a widget that will do this for you. When using the SDKs, see [SDK Usage](#SDK Usage) section below.

*1.* In the portal, navigate to *Configurator > Test Harness*.

*2.* Authenticate as a player you've registered previously.

*3.* Under *Requests*, click on *Upload* and select [GetUploadUrlRequest](/API Documentation/Request API/Misc/GetUploadUrlRequest.md).

<q>**Metadata?** Note that the *GetUploadUrlRequest* has an *uploadData* parameter. You can use this to enter some metadata, which will be stored against the player's uploaded binary content. For this example, you can remove this parameter before submitting the request.</q>

*4.* Remove the *uploadData* parameter and submit the *GetUploadUrlRequest*. You'll see a *GetUploadUrlResponse* in the *Inspector* window and the upload Url is automatically entered into the *URL* field:

![](img/Binary/2.png)

*5.* Under *File*, click *Browse* to select the file you want to upload as binary content to the platform.

*6.* When you've selected the file you want to upload, click *Upload*:
* An *UploadCompleteMessage* shows in the *Inspector* window.
* An *Uploading* button appears at the top of the page and when the upload completes, you can click on this to review your uploads to the platform:

![](img/Binary/3.png)


Being an HTTP POST, this is not done through the WebSocket, but once complete the authenticated WebSocket that was used to request the upload URL will receive an [UploadCompleteMessage](/API Documentation/Message API/Misc/UploadCompleteMessage.md) indicating that the upload was successful:

```
{
  "@class": ".UploadCompleteMessage",
  "messageId": "5832edaf3a32df04983a8960",
  "notification": true,
  "playerId": "5818aef23a32df04ae8d53ed",
  "summary": "Your upload is complete",
  "uploadData": {
    "fileName": "634c80176da1458d965692c87c3a8e68-My Document.txt",
    "uploadId": "634c80176da1458d965692c87c3a8e68",
    "fileSize": 30,
    "origFileName": "My Document.txt",
    "playerId": "5818aef23a32df04ae8d53ed"
  },
  "uploadId": "634c80176da1458d965692c87c3a8e68"
}


```

Within the message is an *uploadData* attribute which contains all the data about the upload:
* If you had used the *uploadData* parameter to submit some metadata with the *GetUploadedRequest*, this would be shown in the *UploadCompleteMessage*. However, you cannot use the *uploadData* parameter to overwrite the system attributes returned in the *UploadCompleteMessage* - even if you had submitted, for example, an *origFileName* with the request, this will not overwrite the system-generated value for this attribute.
* Make sure you hold on to the *uploadId*, because we'll need it in the [next step](#Retrieve the Content).



## Retrieve the Content

The final step is to actually retrieve the content that has been uploaded.

*1.* In the *Test Harness* click *Misc* under *Requests* and select [GetUploadedRequest](/API Documentation/Request API/Misc/GetUploadedRequest.md) which takes an uploadId (which we received from the UploadCompleteMessage):

```
{
  "@class": ".GetUploadedRequest",
  "uploadId":"635ec5dda1bc40b9b53e30618e1d8fff"
}

```

A *GetUploadedResponse* is returned, which contains a URL we can use to download the content. As before, this URL is time-sensitive so don't hang onto it for long - request one as you need it.

```

{
  "@class": ".GetUploadedResponse",
  "size": 30,
  "url": "https://gamesparkstestbinaries.blob.core.windows.net/upload-358719/635ec5dda1bc40b9b53e30618e1d8fff-My%20Document4.txt?sig=AP7P%2BttABetqCBxeq9TfmUL0E5jYa1bVaNFh6WoTYqg%3D&st=2016-11-21T13%3A47%3A21Z&se=2016-11-21T14%3A02%3A21Z&sv=2015-04-05&sp=r&sr=b&gsstage=preview"
}

```


*2.* Go ahead and test the URL you receive by pasting it into your address bar in the browser. You should be able to download the content you uploaded in the earlier step.

<q>**uploadId not Tied to One Player!** The *uploadId* is not tied to a specific player, so if you were to send that *uploadId* to another player, the other player could also use it to request a download URL. This means you can allow your players to share content by sending the *uploadIds* to other players.</q>

## Deleting Uploaded Files

When managing your uploaded files, you can use the [deleteUploadedFile](/API Documentation/Cloud Code API/Cloud Data/SparkFiles.md) *SparkFiles* method to delete uploaded files.

## SDK Usage

### Android and Unity

#### Upload

For completeness we expose the method *getUploadUrlRequest* to build the request object to get a URL to post the upload to. However, there's an additional method we provide called *uploadFile* that takes a file, fileName, and optional metadata about the upload. This wraps the request to get an upload URL and the subsequent upload of the file and presents them as a single operation.

#### Download

As with the upload, we expose the method *getUploadedRequest* to build the request object to get a URL to download the file. However, there's an additional method *getUploadedFile* which takes the *uploadId* and wraps up requesting the download URL and performing the download itself and presents them as a single operation.

### Others

We haven't yet added the above convenience methods for any of the SDKs apart from the Android and Unity SDKs, so for now you'll need to implement the multipart post yourself. We won't go into the details of exactly how to implement this here because there are many great resources already available that cover this. What you do need to know is that the parameter name against which the binary content is posted is *file*.
