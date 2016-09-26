---
src: /API Documentation/Cloud Code API/Player/SparkTeams.md
---

# SparkTeams

Provides access to teams for the current game.

e.g.

<pre rel="highlighter" code-brush="js" contenteditable="false">var team = Spark.getTeams().getTeam(myTeamId);</pre>



## getTeam
_signature_ getTeam(string teamId)</p>
_returns_ [SparkTeam](/API Documentation/Cloud Code API/Player/SparkTeam.md)</p>
Returns a SparkTeam object that represents the team with the given teamId.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var team = Spark.getTeams().getTeam(myTeamId);</pre>

## getTeamByOwnerIdAndTeamType
_signature_ getTeamByOwnerIdAndTeamType(string ownerId, string teamType)</p>
_returns_ [SparkTeam](/API Documentation/Cloud Code API/Player/SparkTeam.md)[]</p>
Returns an array of SparkTeam objects for the given ownerId and teamType.<b>example</b><pre rel="highlighter" code-brush="js" contenteditable="false">var teams = Spark.getTeams().getTeamByOwnerIdAndTeamType(myOwnerId, myTeamType);</pre>

