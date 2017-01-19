---
src: /API Documentation/Cloud Code API/Utilities/SparkBulkScheduler.md
---

# SparkBulkScheduler

Provides access to the bulk scheduler.

<pre rel="highlighter" code-brush="js" contenteditable="false">var bulkScheduler = Spark.getBulkScheduler();</pre>



## submitJobModule

_signature_ submitJobModule(JSON playerQuery, string module, JSON data, number delaySeconds)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Submit a job to be executed by running a Cloud Code module.

<b>params</b>

playerQuery - A query to be run against the player collection to identify the players to execute against

module - A Cloud Code module short code, to be executed against each player

data - Data to be passed in to the Cloud Code module

delaySeconds - The number of seconds in the future to execute the job

<b>returns</b>

The jobId if the job was accepted, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var jobId = Spark.getBulkScheduler().submitJobModule(query, module, data, delaySeconds);</pre>


## submitJobScript

_signature_ submitJobScript(JSON playerQuery, string script, JSON data, number delaySeconds)</p>

_returns_ string</p>

<b>validity</b> All Scripts

Submit a job to be executed by running an ad-hoc script.

<b>params</b>

playerQuery - A query to be run against the player collection to identify the players to execute against

script - A Cloud Code script to be executed against each player

data - Data to be passed in to the script

delaySeconds - The number of seconds in the future to execute the job

<b>returns</b>

The jobId if the job was accepted, or null

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var jobId = Spark.getBulkScheduler().submitJobScript(query, script, data, delaySeconds);</pre>


## cancelJob

_signature_ cancelJob(string jobId)</p>

_returns_ boolean</p>

<b>validity</b> All Scripts

Cancel a previously scheduled bulk job.

<b>params</b>

jobId - The ID of the job to cancel

<b>returns</b>

true if the job was cancelled, false otherwise

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var cancelled = Spark.getBulkScheduler().cancelJob(jobIdToCancel);</pre>


## listBulkJobs

_signature_ listBulkJobs(string[] jobIds)</p>

_returns_ SparkBulkJob[]</p>

<b>validity</b> All Scripts

List previously scheduled bulk jobs.

<b>params</b>

jobIds - The IDs of the jobs to list, or null to list all pending jobs

<b>returns</b>

An array of bulk jobs

<b>example</b>

<pre rel="highlighter" code-brush="js" contenteditable="false">var cancelled = Spark.getBulkScheduler().listBulkJobs(null);</pre>


