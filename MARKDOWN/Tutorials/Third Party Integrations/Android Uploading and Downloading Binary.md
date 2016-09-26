---
nav_sort: 3
src: /Tutorials/Third Party Integrations/Android Uploading and Downloading Binary.md
---

# Android Uploading and Downloading Binary Data

You can upload and download binary data to the GameSparks platform in two ways:
* Manually
* From the SDK

In this tutorial, we'll learn how to do both of these when using the Android client with the GamesSparks platform.

## Manually Uploading and Downloading Data to the Platform

When you have used GameSparks [downloadables](/Documentation/Configurator/Downloadables.md) to upload binary data to specific slots, you can reference them by their unique ShortCodes using the *GetDownloadableResponse* and receive a URL to download them from. If an image is uploaded and the ShortCode is set to 'logo', this will retrieve a URL to download the binary data:

```
GSAndroidPlatform.gs().getRequestBuilder().createGetDownloadableRequest()
        .setShortCode("logo").send(new GSEventConsumer() {
    @Override
    public void onEvent(GSResponseBuilder.GetDownloadableResponse getDownloadableResponse) {
        if (!getDownloadableResponse.hasErrors()) {
            System.out.println("Download URL is " + getDownloadableResponse.getUrl());
        }
    }
});

```

## Uploading and Downloading Binary Data from the SDK

This method is useful for users uploading their content to the platform and with this method you don't need to first create GamesSparks downloadables. An example would be user-created content or a personal profile photo. Instead of ShortCodes, this method relies on *uploadId*. The process has three stages.

### Creating an uploadRequest

The upload [request](/API Documentation/Request API/Misc/GetUploadUrlRequest.md) returns a URL that you can be use to store binary data. Use a HTTP set function to upload your binary data to this URL.

```
GSAndroidPlatform.gs().getRequestBuilder().createGetUploadUrlRequest()
        .send(new GSEventConsumer() {
            @Override
            public void onEvent(GSResponseBuilder.GetUploadUrlResponse getUploadUrlResponse) {
                if (!getUploadUrlResponse.hasErrors()) {
                    System.out.println("upload URL is " + getUploadUrlResponse.getUrl());
                }
            }
        });

```

### Listening for the Upload Complete Message

Once the upload process has taken place, the player will receive a notification in a form of a message. By creating a message handler to listen for these messages, you can intercept and dissect them.

Here's an example of setting up a listener for an upload [message](/API Documentation/Message API/Misc/UploadCompleteMessage.md):

```
GSAndroidPlatform.gs().getMessageHandler()
        .setUploadCompleteMessageListener(new GSEventConsumer() {
    @Override
    public void onEvent(GSMessageHandler.UploadCompleteMessage uploadCompleteMessage) {
        if(uploadCompleteMessage.getNotification()){
            //File uploaded successfully
            System.out.println(uploadCompleteMessage.getUploadId());
        }
    }
});

```

### Obtaining the Uploaded Content

Once the binary content has successfully been uploaded and an *uploadId* has been created for that item, any player will be able to download that binary data using a HTTP get function. By referencing the *uploadId* using the [getUploadedRequest](/API Documentation/Request API/Misc/GetUploadedRequest.md), a response with the URL associated with the item is returned.

```
GSAndroidPlatform.gs().getRequestBuilder().createGetUploadedRequest()
        .setUploadId(uploadId).send(new GSEventConsumer() {
    @Override
    public void onEvent(GSResponseBuilder.GetUploadedResponse getUploadedResponse) {

    }
});

```
