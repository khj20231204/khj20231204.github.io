---
layout: single
title: tomcat 에러
categories: SPRING
tag: []
author_profile: false
---

1. # org.apache.coyote.http11.Http11Processor.service Error parsing HTTP request header
org.apache.coyote.http11.Http11Processor.service Error parsing HTTP request header
 Note: further occurrences of HTTP request parsing errors will be logged at DEBUG level.

<img src="../../imgs/spring/tomcaterror1.png" style="border:3px solid black;border-radius:9px;width:800px">   

https://localhost:8080을 하든데 https에서 s를 없애면 됩니다.   
```
   http://localhost:8080
```