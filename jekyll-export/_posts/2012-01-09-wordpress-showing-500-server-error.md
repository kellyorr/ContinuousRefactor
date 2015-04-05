---
title: WordPress Showing 500 Server error
author: kellyorr
layout: post
permalink: /wordpress-showing-500-server-error/
categories:
  - Software Development
tags:
  - PHP
  - WordPress
---
For several days I would access my blog here to see a HTTP/500 server error.  This would occur when accessing either the administrative console or when accessing the front page of the site.  After some digging I found that the default PHP memory limit was set to 16Mb.  It was recommended to boost the memory limit for WordPress to 128MB.  I did this by adding the single line of code to the `wp-config.php` file.

<pre class="brush: php; title: ; notranslate" title="">@ini_set("memory_limit","16M");
</pre>