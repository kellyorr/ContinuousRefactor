---
title: Redirecting with web.config
author: kellyorr
layout: post
permalink: /redirecting-with-web-config/
categories:
  - Software Development
tags:
  - ASP.NET
---
Here is how to conduct an HTTP 301 Permanent Redirect from one web site to another location using `web.config` in ASP.NET:

<pre class="brush: xml; title: ; notranslate" title="">&lt;configuration&gt;
    &lt;system.webServer&gt;
        &lt;httpRedirect enabled="true" 
                destination="http://www.digitalhoneycomb.com" 
                exactDestination="true" 
                httpResponseStatus="Permanent" /&gt;
    &lt;/system.webServer&gt;
&lt;/configuration&gt;
</pre>