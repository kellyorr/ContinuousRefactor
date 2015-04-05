---
title: FogBugz SQL Maintenance
author: kellyorr
layout: post
permalink: /fogbugz-sql-maintenance/
categories:
  - Software Development
tags:
  - FogBugz
  - Tools
---
I have used and have been an avid fan of FogBugz for years.&nbsp; One quirk that I experience when running on Microsoft SQL Standard or SQL Express is that the database grows very quickly.&nbsp; Even so, it can be reduced back to an acceptable size by running a simple script.&nbsp; I am now running FogBugz 6.1 and using SQL Server 2008 Express, 64-bit. 

Here is the SQL maintenance script:

<pre class="brush: sql; title: ; notranslate" title="">USE FogBugz
GO
ALTER DATABASE FogBugz
SET RECOVERY SIMPLE;
GO
DBCC SHRINKFILE ([FOGBUGZ DATABASE FILE DatabaseName],1);
DBCC SHRINKFILE ([FOGBUGZ LOG FILE LogFileName],1);
GO
ALTER DATABASE FogBugz
SET RECOVERY FULL
GO
</pre>

Since I am running SQL Express edition, there is no built-in support to run maintenance packages, so I use the command line OSQL to run the script above.

Here is the command line:  
[CODE]osql -ic:\tools\fb\_shrink.sql -E -S.\SQLEXPRESS -oc:\tools\fogbugz\_shrink_results.txt[/CODE]

I saved that command in a BAT file and then scheduled using the system scheduled tasks to be executed once daily.