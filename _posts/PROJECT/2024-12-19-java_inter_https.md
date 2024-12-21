---
layout: single
title: Java에서 HTTPS 사용하기
categories: PROJECT
tag: []
---

1. # HTTPS 사용하기
   2차 프로젝트에서는 채팅 서버를 자바 스프링으로 만든 후 EC2에 배포를 했고 클라이언트는 git pages 웹 호스팅을 했고 도메인을 webrtcpj.i-o.kr로 바꾼 상태였습니다.   
   도메인 webrtcpj.i-o.kr이 실행되면 자바스크립트로 구현한 클라이언트 측 내부에서 `SockJS("http://<EC2 주소>/webrtcpjs/test")`이 실행되면서 http로 EC2에 배포된 채팅 서버로 접속을 하게됩니다. 이때 AWS는 보안상 http의 접근을 막게 됩니다. https만 요구를 하는 상황에서 http의 접근은 오류가 발생하게됩니다. 만약  `SockJS("http://<EC2 주소>/webrtcpjs/test")`를 https로 변경하여 `SockJS("https://<EC2 주소>/webrtcpjs/test")`로 접근을 하게되면 트래픽이 서버까지 도달은 하지만 JAVA로 구현한 서버측에 https에 대한 어떤 처리과정도 없기 때문에 채팅에 대한 오류가 발생하게 됩니다.   
   http의 트래픽을 https로 바꾸기 위해서는 <a href="2024-12-13-aws_loadbalancer.md#sslsection">SSL인증</a>이 필요합니다. 


1. # application.properties

   ```yml
      server.port=443
      server.ssl.enabled=true
      server.ssl.key-store=classpath:keystore.p12
      server.ssl.key-store-password=chatserverkey
      server.ssl.key-store-type=PKCS12
      server.ssl.key-alias=chatserverkey
   ```