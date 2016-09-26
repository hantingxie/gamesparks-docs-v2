---
nav_sort: 4
src: /Tutorials/Database Access and Cloud Storage/Uploading Binary Content from Game.md
---

# How to upload binary content directly from your game

The GameSparks platform provides the capability for you to allow players to upload binary content, to be hosted on the GameSparks platform and from there shareable with other players. To do so is fairly simple, but requires a few steps to be completed as follows:

1. Request a URL from the platform to which you can upload the content.
2. Upload the content to the URL obtained in the previous step.
3. Once uploaded you will want the player (or other players) to be able to retrieve the content for use.

In this exercise we'll run through how you do each of the above with the GameSparks API, demonstrated using the [Test Harness](/Documentation/Test Harness/README.md). To finish, there is a brief note on using the GameSparks SDKs to perform these steps (which we've streamlined behind the scenes to make your life easier).

## Get an Upload URL

The first step is to get an upload URL, after all you need somewhere to post your content. If you're following these steps in the Test Harness, these requests are available under the 'Misc' category (make sure you've authenticated as a player before making the first request).

A [GetUploadUrlRequest](/API Documentation/Request API/Misc/GetUploadUrlRequest.md) made by an authenticated player will result in a response containing a 'url' attribute. This is your upload URL, these are one-shot URLs that expire after a matter of minutes so don't hang onto them - if you don't use it right away throw it away and request another one.

```
{
  "@class": ".GetUploadUrlRequest"
}

```
 

```
{
 "@class": ".GetUploadUrlResponse",
 "scriptData": null,
 "url": "https://gsp-aeu000-se04.gamesparks.net/upload/288934CFkBXg/16fc457d-656e-47ea-ad28-00595ec04054/3d3cbd17d2584e8295756d021dd0888b"
}

```

## Upload the Content

Now that you have the upload URL you need to post the file. This is done using a multipart/form-data post - we'd recommend checking it out in the Test Harness as we've provided a widget that will do this for you, and when using the SDKs see the section further down on SDK Usage.

In the Test Harness, once you've made a GetUploadUrlRequest, you should see the upload URL populated within the Requests area. Now click 'Choose File', and select the file you want to upload. Once selected click 'Upload File'.

![](img/Binary/1.png)

Being an HTTP POST, this is not done through the WebSocket, but once complete the authenticated WebSocket that was used to request the upload URL will receive an [UploadCompleteMessage](/API Documentation/Message API/Misc/UploadCompleteMessage.md) indicating that the upload was successful.

```
{
 "@class": ".UploadCompleteMessage",
 "messageId": "55db13cce4b0548f701b3d66",
 "notification": true,
 "summary": "Your upload is complete",
 "playerId": "552bd84ce4b0e4d939d05899",
 "uploadData": {
  "fileSize": 250011,
  "playerId": "552bd84ce4b0e4d939d05899",
  "uploadId": "3d3cbd17d2584e8295756d021dd0888b",
  "origFileName": "test.jpg",
  "fileName": "3d3cbd17d2584e8295756d021dd0888b-test.jpg"
 },
 "uploadId": "3d3cbd17d2584e8295756d021dd0888b"
}

```

Within the message is an attribute 'uploadData' which contains all the data about the upload. Hold onto the uploadId, as we'll need it in the next step.

## Retrieve the Content

The final step is to actually retrieve the content that has been uploaded. This is achieved using a [GetUploadedRequest](/API Documentation/Request API/Misc/GetUploadedRequest.md) which takes an uploadId (which we received from the UploadCompleteMessage).

```

{
 "@class": ".GetUploadedRequest",
 "uploadId": "3d3cbd17d2584e8295756d021dd0888b"
}

```

The response to this request contains a URL we can use to download the content. As before, this URL is time-sensitive so don't hang onto it for long - request one as you need it.

```
{
 "@class": ".GetUploadedResponse",
 "scriptData": null,
 "size": 250011,
 "url": "https://gamesparksbetabinaries.blob.core.windows.net/upload-288934/3d3cbd17d2584e8295756d021dd0888b-test.jpg?sp=r&sr=b&sv=2012-02-12&se=2015-08-24T13%3A04%3A42Z&st=2015-08-24T12%3A49%3A42Z&sig=fFFWxoNmmt0tdSjd8uTRTOkYn0zWWEOg7UVIbEvABpo%3D"
}

```

Go ahead and test the URL you receive by pasting it into your address bar in the browser. You should be able to download the content you uploaded in the earlier step. The uploadId is not tied to a specific player, so if you were to send that uploadId to another player they too could use it to request a download URL. This means you can allow your players to share content by sending the uploadIds to other players.

## Deleting Uploaded Files

When managing your uploaded files, you can use the [deleteUploadedFile](/API Documentation/Cloud Code API/Cloud Data/SparkFiles.md) *SparkFiles* method to delete uploaded files.</q>

## SDK Usage

### Android and Unity

#### Upload

For completeness we expose the method getUploadUrlRequest to build the request object to get a URL to post the upload to, however there is an additional method we provide called uploadFile that takes a file, fileName and optional metadata about the upload. This wraps the request to get an upload URL and the subsequent upload of the file and presents them as a single operation.

#### Download

As with the upload we expose the method getUploadedRequest to build the request object to get a URL to download the file however there is an additional method getUploadedFile which takes the uploadId and wraps up requesting the download URL and performing the download itself and presents them as a single operation.

### Others

We haven't yet added the above convenience methods for any of the SDKs apart from the Android and Unity SDKs, so for now you'll need to implement the multipart post yourself. We won't go into the details of exactly how to implement this here as there are many great resources already available that cover this. What you do need to know is that the parameter name against which the binary content is posted is file.
