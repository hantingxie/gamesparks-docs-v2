---
src: /API Documentation/Cloud Code API/Cloud Data/SparkFiles.md
---

# SparkFiles

Provides access uploaded files along with downloadables



## deleteUploadedFile
_signature_ deleteUploadedFile(string uploadId)</p>
_returns_ boolean</p>
<b>validity</b> All ScriptsDeletes a previously uploaded file by uploadId<b>params</b>uploadId - the id of the uploaded file<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getFiles().deleteUploadedFile("myUploadId");</pre>

## uploadedXml
_signature_ uploadedXml(string uploadId)</p>
_returns_ [SparkXmlReader](/API Documentation/Cloud Code API/Cloud Data/SparkXmlReader.md)</p>
<b>validity</b> All ScriptsProvides access to an uploaded file via a SparkXmlReader interface<b>params</b>uploadId - the id of the uploaded file<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var reader = Spark.getFiles().uploadedXml("myUploadId");</pre>

## uploadedJson
_signature_ uploadedJson(string uploadId)</p>
_returns_ JSON</p>
<b>validity</b> All ScriptsProvides access to an uploaded file via a JSON object<b>params</b>uploadId - the id of the uploaded file<b>returns</b>A JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var reader = Spark.getFiles().uploadedJson("myUploadId");</pre>

## downloadableXml
_signature_ downloadableXml(string shortCode)</p>
_returns_ [SparkXmlReader](/API Documentation/Cloud Code API/Cloud Data/SparkXmlReader.md)</p>
<b>validity</b> All ScriptsProvides access to a downloadable file via a SparkXmlReader interface<b>params</b>shortCode - the short code for the downloadable file<b>returns</b><b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var reader = Spark.getFiles().downloadableXml("shortCode");</pre>

## downloadableJson
_signature_ downloadableJson(string shortCode)</p>
_returns_ JSON</p>
<b>validity</b> All ScriptsProvides access to a downloadable file via a JSON object<b>params</b>shortCode - the short code for the downloadable file<b>returns</b><b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var reader = Spark.getFiles().downloadableJson("shortCode");</pre>

