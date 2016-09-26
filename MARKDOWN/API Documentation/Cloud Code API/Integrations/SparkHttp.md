---
src: /API Documentation/Cloud Code API/Integrations/SparkHttp.md
---

# SparkHttp

Provides access to a HTTP client object.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var httpSender = Spark.getHttp("http://somehost");</pre>



## setBasicAuth
_signature_ setBasicAuth(string username, string password)</p>
_returns_ [SparkHttp](/API Documentation/Cloud Code API/Integrations/SparkHttp.md)</p>
Sets credentials to be used for Basic Auth<b>params</b>userName - the username to usepassword - the password to use<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).setBasicAuth("myusername", "mypassword");</pre>

## setHeaders
_signature_ setHeaders(JSON headers)</p>
_returns_ [SparkHttp](/API Documentation/Cloud Code API/Integrations/SparkHttp.md)</p>
Add custom header to the request<b>params</b>headers - A JSON object<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).setHeaders({"X-Custom-header":"1234"});</pre>

## get
_signature_ get()</p>
_returns_ [SparkHttpResponse](/API Documentation/Cloud Code API/Integrations/SparkHttpResponse.md)</p>
Perform a HTTP GET request<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var response = Spark.getHttp(url).get();</pre>

## postForm
_signature_ postForm(JSON form)</p>
_returns_ [SparkHttpResponse](/API Documentation/Cloud Code API/Integrations/SparkHttpResponse.md)</p>
Perform a HTTP POST using a JSON form object<b>params</b>form - the HTTP form data<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).postForm(form);</pre>

## postXml
_signature_ postXml(XMLObject form)</p>
_returns_ [SparkHttpResponse](/API Documentation/Cloud Code API/Integrations/SparkHttpResponse.md)</p>
Perform a HTTP POST using an XML form object<b>params</b>form - the HTTP form data<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).postXml(xmlForm);</pre>

## postJson
_signature_ postJson(JSON form)</p>
_returns_ [SparkHttpResponse](/API Documentation/Cloud Code API/Integrations/SparkHttpResponse.md)</p>
Perform a HTTP POST using a JSON form object<b>params</b>form - the HTTP form data<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).postJson(jsonForm);</pre>

## postString
_signature_ postString(string data)</p>
_returns_ [SparkHttpResponse](/API Documentation/Cloud Code API/Integrations/SparkHttpResponse.md)</p>
Perform a HTTP POST using a string<b>params</b>data - the HTTP POST data<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getHttp(url).postString(data);</pre>

