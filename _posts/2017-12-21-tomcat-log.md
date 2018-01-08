---
title: Tomcat log file introduce
categories:
  - Server
tags:
  - tomcat
---

### What does localhost_access_log file do?

localhost_access_log.year-month-date.txt file

localhost access log in tomcat contains the information associated with a request i.e., ip address, time, request method(GET or POST) and the resource for which the request is coming.


### What does Catalina.out do?

Catalina.out simply contains everything that is written to Tomcat's "System.out" and "System.err".

The name "catalina.out" comes from the catalina.sh script that is conventionally used to launch Tomcat. If you want to change the name ... or do something funky with your out/err streams ... you can hack the script, or replace it with an alternative launch script.

### Reference
http://z724130632.iteye.com/blog/2352869