---
title: Determining the SQL version and release
author: kellyorr
layout: post
permalink: /determining-the-sql-version-and-release/
categories:
  - Software Development
tags:
  - SQL
---
For years when I needed to determine if a service pack was installed on SQL Server 2000 or SQL Server 2005, I would check the build number and ten search the web to find what the build number was for the latest service pack. Today I was going through the same routine, but when I searched Google, I found a SQL query that would more directly reveal the version and release:

<pre class="brush: sql; title: ; notranslate" title="">SELECT  
   SERVERPROPERTY('productversion'), 
   SERVERPROPERTY ('productlevel'), 
   SERVERPROPERTY ('edition')
</pre>

Here is the [Microsoft KB article][1].  
Here is a [chart of all SQL Versions][2], their names and release dates.

 [1]: http://support.microsoft.com/kb/321185
 [2]: http://www.sqlteam.com/article/sql-server-versions
