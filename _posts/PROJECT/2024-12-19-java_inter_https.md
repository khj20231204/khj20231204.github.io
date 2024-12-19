---
layout: single
title: Java에서 HTTPS 사용하기기
categories: PROJECT
tag: []
---

1. # 



1. # application.properties

   ```yml
      server.port=443
      server.ssl.enabled=true
      server.ssl.key-store=classpath:keystore.p12
      server.ssl.key-store-password=chatserverkey
      server.ssl.key-store-type=PKCS12
      server.ssl.key-alias=chatserverkey
   ```