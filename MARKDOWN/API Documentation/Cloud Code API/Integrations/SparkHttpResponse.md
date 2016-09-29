# SparkHttpResponse

Represents the response form the HTTP call.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var headers = response.getHeaders();</pre>


## getHeaders
_signature_ getHeaders()</p>
_returns_ JSON</p>

Returns the headers from the response.

<b>returns</b>

A JSON object containing the headers

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var headers = response.getHeaders();</pre>

## getResponseCode
_signature_ getResponseCode()</p>
_returns_ number</p>

Returns the response code.

e.g. 200

<b>returns</b>

the HTTP status code

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var statusCode = response.getResponseCode();</pre>

## getResponseString
_signature_ getResponseString()</p>
_returns_ string</p>

Returns the body from the response.

<b>returns</b>

A string representing the body of the response.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var body = response.getResponseString();</pre>

## getResponseXml
_signature_ getResponseXml()</p>
_returns_ JSON</p>

Returns the body from the response as XML.

<b>returns</b>

A JSON representing the body of the response.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var body = response.getResponseXml();</pre>

## getResponseJson
_signature_ getResponseJson()</p>
_returns_ JSON</p>

Returns the body from the response as JSON.

<b>returns</b>

A string representing the body of the response.

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

<pre rel="highlighter" code-brush="js" contenteditable="false">var body = response.getResponseJson();</pre>

