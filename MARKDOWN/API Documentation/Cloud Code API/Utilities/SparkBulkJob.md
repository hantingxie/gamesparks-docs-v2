---
src: /API Documentation/Cloud Code API/Utilities/SparkBulkJob.md
---

# SparkBulkJob

An object that represents a bulk job.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var bulkJob = Spark.getBulkJobScheduler().listBulkJobs(null)[0];</pre>



## getId
_signature_ getId()</p>
_returns_ string</p>
Returns the ID of this bulk job.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">Spark.getBulkJobScheduler().listBulkJobs(null)[0].getId();</pre>

## getActualCount
_signature_ getActualCount()</p>
_returns_ number</p>
The actual count of players affected by the bulk job

## getCompleted
_signature_ getCompleted()</p>
_returns_ date</p>
The time at which the bulk job completed execution

## getCreated
_signature_ getCreated()</p>
_returns_ date</p>
The time at which the bulk job was created

## getData
_signature_ getData()</p>
_returns_ JSON</p>
Data to be passed into the Module or Script

## getDoneCount
_signature_ getDoneCount()</p>
_returns_ number</p>
The number of players processed by the bulk job

## getErrorCount
_signature_ getErrorCount()</p>
_returns_ number</p>
The number of errors encountered whilst running the Module or Script for players

## getEstimatedCount
_signature_ getEstimatedCount()</p>
_returns_ number</p>
The estimated count of players affected by the bulk job

## getModuleShortCode
_signature_ getModuleShortCode()</p>
_returns_ string</p>
The Cloud Code Module to run for each player

## getPlayerQuery
_signature_ getPlayerQuery()</p>
_returns_ JSON</p>
The query to identify players to perform the bulk job on

## getScheduledTime
_signature_ getScheduledTime()</p>
_returns_ date</p>
The time at which the job was scheduled to run

## getScript
_signature_ getScript()</p>
_returns_ string</p>
The Cloud Code script to run for each player

## getStarted
_signature_ getStarted()</p>
_returns_ date</p>
The time at which the bulk job started to execute

