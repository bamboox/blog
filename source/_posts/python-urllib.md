---
title: python url admin:password
date: 2018-01-02 22:49:50
tags: python
categories: python 
---

### curl 

curl  "http://admin:random_password@10.189.195.39:2999/api/dashboards/db/bls_mysql_metrics"

### python
```
import urllib2, base64

request = urllib2.Request("http://api.foursquare.com/v1/user")
base64string = base64.b64encode('%s:%s' % (username, password))
request.add_header("Authorization", "Basic %s" % base64string)   
result = urllib2.urlopen(request)
body=result.read()
```
<!--more-->

