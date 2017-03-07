---
nav_sort: 8
src: /Tutorials/Game Engine Integrations/Unity Uploading and Retrieving Images.md
---

# Uploading and Retrieving Images from Unity to GameSparks

## Introduction

If you are using the Unity client with the GameSparks platform, there might be occasions where you need to upload images to GameSparks. For instance, to store:
* Profile pictures.
* User-made levels, screenshots, and so on.
* Any sort of binary save data.

This tutorial shows you how to do this.  

## Sample Script

Here's a sample script that takes a screenshot, uploads it to GameSparks, and then allows you to re-download it:

```

using UnityEngine;
using System.Collections;
using GameSparks.Api.Requests;

using GameSparks.Api.Messages;

public class UploadFile : MonoBehaviour {

    private string lastUploadId;
    public Texture2D downloadedImage;

    public void Start()
    {
        //We will be passing all our messages to a listener function
        UploadCompleteMessage.Listener += GetUploadMessage;
    }

    //This will get our upload url and on the response we will start our coroutine to take the screenshot
    public void UploadScreenShot () {
        new GetUploadUrlRequest().Send((response) =>
        {
            //Start coroutine and pass in the upload url
            StartCoroutine(UploadAFile(response.Url));  
        });
    }

    //Our coroutine takes a screenshot of the game
    public IEnumerator UploadAFile(string uploadUrl)
    {

        yield return new WaitForEndOfFrame();

        int width = Screen.width;
        int height = Screen.height;
        Texture2D tex = new Texture2D(width, height, TextureFormat.RGB24, false);
        tex.ReadPixels(new Rect(0, 0, width, height), 0, 0);
        tex.Apply();
        //This basically takes a screenshot

        byte[] bytes = tex.EncodeToPNG(); //Can also encode to jpg, just make sure to change the file extensions down below
        Destroy(tex);

        // Create a Web Form, this will be our POST method's data
        var form = new WWWForm();
        form.AddField("somefield", "somedata");
        form.AddBinaryData("file", bytes, "screenshot.png", "image/png");

    //POST the screenshot to GameSparks
        WWW w = new WWW(uploadUrl, form);
        yield return w;

        if (w.error != null)
        {
            Debug.Log(w.error);
        }
        else
        {
            Debug.Log(w.text);
        }
    }

    //This will be our message listener, this will be triggered when we successfully upload a file
    public void GetUploadMessage(GSMessage message)
    {
        //Every time we get a message
        Debug.Log(message.BaseData.GetString("uploadId"));
        //Save the last uploadId
        lastUploadId = message.BaseData.GetString("uploadId");
    }

    //When we want to download our uploaded image
    public void DownloadAFile()
    {
        //Get the url associated with the uploadId
        new GetUploadedRequest().SetUploadId(lastUploadId).Send((response) =>
            {
                //pass the url to our coroutine that will accept the data
                StartCoroutine(DownloadImage(response.Url));
            });
    }


    public IEnumerator DownloadImage(string downloadUrl)
    {
        var www = new WWW(downloadUrl);

        yield return www;

        downloadedImage = new Texture2D(200, 200);

        www.LoadImageIntoTexture(downloadedImage);
    }
}


```
