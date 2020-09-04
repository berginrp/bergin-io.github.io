---
id: 189
title: How to delete class from Production org
date: 2018-07-27T11:40:44-04:00
author: Bergin Panimayam
layout: post
guid: http://www.bergin.in/?p=189
permalink: /2018/07/27/how-to-delete-class-from-production-org/
avada_post_views_count:
  - "0"
categories:
  - Apex
tags:
  - Apex
  - Class
  - Production
  - Salesforce
---
This is a common question that comes up and it&#8217;s very simple to do. From your IDE, in your -meta.xml file, change the <status> to Deleted.

> <span style="font-family: Menlo;"><span style="color: #000000;"> <?xml version=&#8221;1.0&#8243; encoding=&#8221;UTF-8&#8243;?></span><br /> <span style="color: #000000;"><ApexClass xmlns=&#8221;http://soap.sforce.com/2006/04/metadata&#8221;></span><br /> <span style="color: #000000;">    <apiVersion>41.0</apiVersion></span><br /> <span style="color: #000000;">    <span style="color: #339966;"><status>Deleted</status></span></span><br /> <span style="color: #000000;"></ApexClass></span></span>

Make sure you check the code coverage and take necessary action.<span style="font-family: Menlo;"><br /> </span>