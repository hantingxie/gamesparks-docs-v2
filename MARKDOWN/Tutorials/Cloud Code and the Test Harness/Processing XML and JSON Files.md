---
nav_sort: 12
src: /Tutorials/Cloud Code and the Test Harness/Processing XML and JSON Files.md
---

# How to Process XML and JSON files

You can use Cloud Code to process both XML files and JSON files. These may be delivered by a player using the [GetUploadUrlRequest](/API Documentation/Request API/Misc/GetUploadUrlRequest.md) model or be delivered via SFTP to the server from a third party.

## Processing XML Files

Both [UploadCompleteMessage](/API Documentation/Message API/Misc/UploadCompleteMessage.md) and the "File Delivered" Cloud Code scripts have access to an attribute that allows you to get the uploaded file so you can process it:

```  
    var uploadedXml = Spark.uploadedXml( Spark.data.uploadId );

```

When you have obtained this object, you are ready to start processing.

There are 2 models for XML files processing:
* Full document
* Streaming. Use streaming when your document might be large, because loading the whole document into memory can take some time.

## Full document processing

When you have obtained the uploadedXml object, you can get the contents of the XML for further processing using the following function:

```
    var rootElement = uploadedXml.getXml();

```
</br>
<q>**Important!** The rootElement object is an [ECMAScript for XML (E4X)](http://en.wikipedia.org/wiki/ECMAScript_for_XML) object that can be processed using JavaScript.</q>

## Stream Processing

For larger documents, you can let the GameSparks platform read the document, and the platform can callback into a custom function when a particular element path is found. In your callback function you will then call *uploadedXml.getElement();* which will give you access to the element that has been located.


## E4X Reference

This section shows you how to process the following example XML file:

```  
    <breakfast_menu>
            <starts>06:00</starts>
            <ends>11:00</ends>
    	<food id="1" price="5.95">
    		<name>Belgian Waffles</name>
    		<description>Two of our famous Belgian Waffles with plenty of real maple syrup</description>
    		<calories>650</calories>
    	</food>
    	<food id="2" price="7.95">
    		<name>Strawberry Belgian Waffles</name>
    		<description>Light Belgian waffles covered with strawberries and whipped cream</description>
    		<calories>900</calories>
    	</food>
    </breakfast_menu>

```
<q>**Note:** Remember that for this example the rootElement object is an E4X object!</q>

To access an element you can use dot notation to navigate through the document:

```
    var childElement = rootElement.starts;

```

To access the text of an element, you can use the *text()* method:

```    
    var startTime = rootElement.starts.text();

```

For repeating items, you can use array notation (0 based) to access an element by index:

```  
    var secondFood = uploadedXml.food[1]

```

To access an attribute, you can use the *@* symbol as the final part of your dot notation:

```  
    var secondPrice = uploadedXml.food[1].@price

```

To iterate over attributes, you can use a standard for construct:

```    
    for( var n = 0 ; n < rootElement.food.length() ; n++ )
    {
         var foodElement = rootElement.food[ n ];
    }

```

## Processing JSON Files

JSON processing is always in full document mode. When you have the handle on the JSON document you can use it as you would any JSON object.

```  
    var uploadedJson = Spark.uploadedJson( Spark.data.uploadId );

```
