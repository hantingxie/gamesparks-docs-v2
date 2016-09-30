---
src: /API Documentation/Cloud Code API/Cloud Data/SparkXmlReader.md
---

# SparkXmlReader

Provides read only access to an Xml document in gamesparks storage.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var myXmlReader = Spark.uploadedXml("7359237762da4245add41e44bc994cdd");</pre>

or

<pre rel="highlighter" code-brush="js" contenteditable="false">var myXmlReader = Spark.downloadableXml("SHORTCODE");</pre>


## registerCallback
_signature_ registerCallback(string path, Function startCallback)</p>
_returns_ void</p>

Registers a function to be called when a given element is found.

<b>params</b>

path - A dot notated path representing the element to attach to

function - Your javascript function that should be called when the element is found

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">uploadedXml.registerCallback("catalog.book", processBookElement);</pre>

## process
_signature_ process()</p>
_returns_ void</p>

Processes each document element and triggers any registered callback

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">uploadedXml.process();</pre>

## getElement
_signature_ getElement()</p>
_returns_ JSON</p>

Returns the current element in the document, generally only useful during callbacks

The returned element only contains the element name and any attributes, it does not include children

<b>returns</b>

The current element

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var element = uploadedXml.element;</pre>

## getXml
_signature_ getXml()</p>
_returns_ JSON</p>

Returns the current element in the document as a complete xml structure including all children

<b>returns</b>

The current element as a document

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var element = uploadedXml.xml;</pre>

