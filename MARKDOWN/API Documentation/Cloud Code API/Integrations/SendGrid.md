# SendGrid

Provides the ability to send emails via <a href="http://sendgrid.com/">SendGrid</a>.
You need to have already set up a SendGrid account, when acessing send grid via gamesparks you need to provide your sendgrid username & password
e.g.
<pre rel="highlighter" code-brush="js" contenteditable="false">var mySendGrid = Spark.sendGrid("userName", "password");</pre>


## addTo

_signature_ addTo(string email, string name)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Adds a recipient to this email
<b>params</b>
email - The email address of the recipient
query - The name of the recipient (optional)
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.addTo("info@gamesparks.com", "GameSparks")</pre>

## send

_signature_ send()</p>
_returns_ string</p>

Sends this email, this step should be performed after configuring the email fully
<b>returns</b>
The response from SendGrid
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.send();</pre>

## setFrom

_signature_ setFrom(string email, string name)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets the from address of this email
<b>params</b>
email - The email address of the sender
query - The name of the sender (optional)
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setFrom("info@gamesparks.com", "GameSparks")</pre>

## setReplyTo

_signature_ setReplyTo(string email)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets the replyTo address of this email
<b>params</b>
email - The email address to replyTo
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setReplyTo("info@gamesparks.com")</pre>

## setBcc

_signature_ setBcc(string bcc)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets a bcc address to this email. SendGrid only allows one address in this field
<b>params</b>
email - The email address to add as bcc
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setBcc("info@gamesparks.com")</pre>

## setSubject

_signature_ setSubject(string subject)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets the subject of this email
<b>params</b>
subject - The subject of the email
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setSubject("Hello from GameSparks")</pre>

## setText

_signature_ setText(string text)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets the text body of this email. If html is set this value is ignored.
<b>params</b>
text - The body of the email
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setText("Welcome to using SendGrid via GameSparks")</pre>

## setHtml

_signature_ setHtml(string html)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Sets the html body of this email.
<b>params</b>
html - The html body of the email
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.setHtml("<b>Welcome to using SendGrid via GameSparks</b>")</pre>

## addUploaded

_signature_ addUploaded(string uploadId)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Adds an uploaded file to the email as an attachment
<b>params</b>
uploadId - The id of the uploaded file
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.addUploaded("7359237762da4245add41e44bc994cdd")</pre>

## addDownloadable

_signature_ addDownloadable(string shortCode)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Adds an downloadable file to the email as an attachment
<b>params</b>
shortCode - The shortCode of the downloadable
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.addDownloadable("SHORTCODE")</pre>

## addHeader

_signature_ addHeader(string key, string value)</p>
_returns_ [SendGrid](/API Documentation/Cloud Code API/Integrations/SendGrid.md)</p>

Adds an custom SMTP header to this email
<b>params</b>
name - The header name to set
value - The value to set for the header
<b>returns</b>
This SendGrid object
<b>example</b>
<pre rel="highlighter" code-brush="js" contenteditable="false">mySendGrid.addHeader("X-Sent-Using", "SendGrid-API")</pre>
