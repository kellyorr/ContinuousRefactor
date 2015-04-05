---
title: Creating Website Redirectors with AWS S3 and Route 53
author: kellyorr
layout: post
permalink: /creating-website-redirectors-with-aws-s3-and-route-53/
categories:
  - Uncategorized
---
Many times I have several domain names that I want to redirect to a single website.  Once the user gets delivered to the website, I want a common FQDN shown in the browser, such as www.OfficialWebSite.com.  This can easily be done using Amazon Web Services  web-enabled S3 buckets and Route 53 DNS services.

**Setup a website in an AWS S3 bucket**

  1. In the AWS Management Console, navigate to S3 and click the &#8216;Create Bucket&#8217; button.
  2. Specify the bucket name to correspond to the FQDN of the site to redirect, for example: www.MarketingName.net.
  3. Create a simple placeholder index.html file on your desktop and upload this file into the newly created S3 bucket by clicking the &#8216;Upload&#8217; button.

<pre class="brush: plain; title: ; notranslate" title="">&lt;html&gt;
&lt;/html&gt;
</pre>

**Configure the AWS3 bucket**

  1. Select the file in AWS and click the &#8216;Properties&#8217; button.
  2. Select the &#8216;Metadata&#8217; tab at the bottom and click &#8216;Add more metadata&#8217;.
  3. Select the &#8216;Website Redirect Location&#8217; key and specify the full location of the new website, in this case: http://www.OfficialWebSite.com.  Click &#8216;Save&#8217;.
  4. Select the www.MarketingName.net bucket in S3.
  5. Select &#8216;Permissions&#8217; in the Properties panel and click &#8216;Add bucket policy&#8217;.
  6. Copy and paste in the following policy.

<pre class="brush: plain; title: ; notranslate" title="">{
 "Version": "2008-10-17",
 "Statement": [
 {
 "Sid": "PublicReadForGetBucketObjects",
 "Effect": "Allow",
 "Principal": {
 "AWS": "*"
 },
 "Action": "s3:GetObject",
 "Resource": "arn:aws:s3:::www.OfficialWebSite.com/*"
 }
 ]
}
</pre>

**Enable and Save the Website**

  1. Select &#8216;Website&#8217; in the Properties panel.
  2. Check the &#8216;Enabled&#8217; checkbox.
  3. Specify &#8216;index.html&#8217; for the &#8216;Index Document&#8217; value.  Click &#8216;Save&#8217;.
  4. Copy the value from the  &#8216;Endpoint&#8217; field.

**Setup the DNS records on Route 53**

  1. In the AWS Management Console, navigate to Route 53 and click the &#8216;Create Hosted Zone&#8217; button.
  2. Type in the domain name, such as MarketingName.Net into the &#8216;Domain Name&#8217; field.
  3. Click the &#8216;Go to Record Sets&#8217; button.
  4. Click &#8216;Create Record Set&#8217;
  5. Enter &#8216;www&#8217; in the &#8216;Name&#8217; field.
  6. Select &#8216;CNAME&#8217; for &#8216;Type&#8217;.
  7. Paste the value from the S3 bucket website &#8216;Endpoint&#8217; field into the Alias &#8216;Value&#8217; field.  Be sure to remove the protocol prefix (http://) and the trailing slash (/), for example: www.MarketingName.Net.s3-website-us-east-1.amazonaws.com.
  8. Click &#8216;Save Record Set&#8217;
  9. Be sure to point the domain record at your registrar to point to the AWS Route 53 DNS services for your this entry.

**Test the redirector**

  1. First try to navigate to the bucket website endpoint, in this case: https://www.OfficialWebsite.com
  2. If that works, then try to access the new redirector, in this case: http://www.MarketingName.Net.