---
title: Reducing the size of a SQL transaction log
author: kellyorr
layout: post
permalink: /reducing-the-size-of-a-sql-transaction-log/
categories:
  - Software Development
tags:
  - SQL
---
I use Microsoft SQL Server quite a bit and have been stuck numerous times on an ever growing transaction log.  After much pounding on the server this evening I once again found the magic commands.  The commands are executed in Query Analyzer or Management Studio after a full backup of the database.

<pre class="brush: sql; title: ; notranslate" title="">BACKUP LOG &lt;database_name&gt; WITH TRUNCATE_ONLY
DBCC SHRINKFILE(&lt;logical file name&gt;,0)
</pre>

With a command line backup:

<pre class="brush: sql; title: ; notranslate" title="">BACKUP DATABASE &lt;database_name&gt; TO "&lt;path to backup location&gt;"
BACKUP TRAN &lt;database_name&gt; TO "path to backup location&gt;"
DBCC SHRINKFILE 0, TRUNCATEONLY
BACKUP LOG &lt;database_name&gt; WITH TRUNCATE_ONLY
DBCC SHRINKFILE('&lt;logical file name&gt;',0)
</pre>

You can get the actual database name and logical file names by examining the contents of the sysfiles table:

<pre class="brush: sql; title: ; notranslate" title="">SELECT * FROM SYSFILES
</pre>