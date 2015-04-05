---
title: Rescuing a locked out Amazon EC2 instance
author: kellyorr
layout: post
permalink: /rescuing-a-locked-out-amazon-ec2-virtual-machine/
categories:
  - Uncategorized
---
One of my projects uses Amazon EC2 for Windows Server machine virtualization. As part of hardening the instance, I changed the Remote Desktop/RDP port to a non-standard port, updated the Security Group to allow access to the new port and rebooted. It wasn&#8217;t until I tried to access the instance did I realize that I had forgotten to also update the Windows Firewall rules to include the port.  But now I was locked out of the instance and could login to allows myself access again.

It was time to call Amazon Technical Support. I added [Developer Level][1] of Amazon Premium Support to my account and opened a ticket. I expected a response the next day within their 12 hour service level agreement, but was surprised to get a response on the ticket within the hour. Unfortunately Technical Support could not just attach to the instance and revert the changes I had made to the registry, reboot and let me back into the server. However, they did include a detail set of instructions on how I could revert the change. The objective is to use another EC2 instance to mount the /dev/sda1 volume that contains the registry of the locked out instance.

Step 1: Create a new EC2 instance of similar type and operating system in the same zone as the EBS volume. At first I tried to use another instance that I had already built, but it was not in the same zone as the EBS I needed to mount. So, I simply created another instance that I named &#8216;Rescue&#8217; and used it.

Step 2: Stop the locked-out instance. Detach the root (/dev/sda1) EBS volume and attach to the Rescue instance as a xvd_ volume

Step 3: Log in to the Rescue instance and use REGEDIT to perform the following:  
&#8211; Run REGEDIT  
&#8211; place the current selection on HLKM  
&#8211; File->Load Hive  
&#8211; Select one of the {Windows Root}\system32\config\ files  
&#8211; Name is soemething like &#8220;old_system&#8221;.  
&#8211; The file will be loaded in HKLM\old_system.  
&#8211; You can now read and edit the registry hive.

Step 4: Once the necessary changes have been made:  
&#8211; Stop the Rescue instance  
&#8211; Detach the EBS volume  
&#8211; Reattach it to the original instance as root (/dev/sda1)  
When I started the original instance back up with the EBS volume I was still not able to gain access. After reviewing the Security Groups and configuration again, I realized that the Elastic IP address was not associated to the EC2 instance. I associated it and was able to again access the server.

Here are the lessons learned during this incident and recovery process  
1) When modifying access ports, add the port number to both the Amazon Security Group and the Windows Firewall  
2) Elastic IP needs to be associated to the EC2 instance each time it is stopped and started, but not each time the instance operating system is rebooted  
3) The &#8216;Refresh&#8217; button in the AWS Management Console is key but on the EBS volumes screen and on Elastic IPs screen. If the status or the configuratio is not what you expect, click the &#8216;Refresh&#8217; button.  
4) When creating new EC2 instances to mount existing EBS volumes, they need to be in the same zone.

 [1]: http://aws.amazon.com/premiumsupport/