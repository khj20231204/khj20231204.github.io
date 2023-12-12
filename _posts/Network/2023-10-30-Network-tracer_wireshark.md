---
layout: single
title: tracer/Wireshark
categories: Network
tag: [tracer, wireshark]
---

1. # tracer(구글과 통신)

   구글 DNS IP주소 : 8.8.8.8   
   
   ```
      C:\Users\natis>tracert 8.8.8.8

      최대 30홉 이상의
      dns.google [8.8.8.8](으)로 가는 경로 추적:

        1     6 ms     8 ms     8 ms  192.168.45.1
        2    25 ms    17 ms    18 ms  211.109.35.1
        3    17 ms     7 ms     7 ms  100.93.7.185
        4    20 ms     5 ms     8 ms  100.93.6.1
        5    18 ms     7 ms     7 ms  10.120.0.84
        6    28 ms    17 ms    17 ms  10.222.35.114
        7    18 ms    18 ms    17 ms  10.222.10.85
        8   257 ms   198 ms    99 ms  142.250.163.48
        9    47 ms    38 ms    38 ms  192.178.46.145
       10    48 ms    47 ms    47 ms  108.170.235.5
       11    45 ms    38 ms    49 ms  dns.google [8.8.8.8]

      추적을 완료했습니다.
   ```   
   192.168.45.1, 211.109.35.1,.. 전부 하나의 네트워크 대역   
   
1. # Wireshark
   - 다운 받기   
   https://www.wireshark.org/   
   <img src="../../imgs/network/wireshark.png " style="border:3px solid black;border-radius:9px;width:700px">   

   - 어탭터 선택   
   <img src="../../imgs/network/wireshark_display.png " style="border:3px solid black;border-radius:9px;width:800px">   
   wi-fi 더블클릭   

   - http로 검색   
   <img src="../../imgs/network/wireshark_http.png " style="border:3px solid black;border-radius:9px;width:800px">   
   이더넷, IPv4, TCP, http 접속 순서에 따른 프로토콜을 확인할 수 있습니다.   