---
layout: single
title: OSI 7계층 vs TCP/IP
categories: Network
tag: [패킷, 캡슐화, 세그먼트, 프레임]
---

1. # OSI

   <table style="font-size:12px;width:900px">
      <tr>
         <td style="font-weight:bold">OSI 7계층</td>
         <td style="font-weight:bold;color:gray">역할</td>
         <td style="font-weight:bold;color:gray">PDU</td>
         <td style="width:150px;font-weight:bold;color:gray">프로토콜</td>
         <!-- <td style="width:80px;font-weight:bold;color:gray">포트번호</td> -->
         <td style="width:60px;font-weight:bold;color:gray">주소 체계</td>
         <td style="width:80px;font-weight:bold;color:gray">장비</td>
         <td style="font-weight:bold">TCP/IP</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Applicaton(응용)</td>
         <td>소프트웨어, UserInterface 제공</td>
         <td rowspan=3>Message</td>
         <td rowspan=3>FTP TCP 20,21<br>Telnet TCP 23<br>SMTP TCP 25<br>HTTP TCP 80<br>HTTPS TCP 443<br>DHCP UDP 67,68<br>SNMP UDP 161,162<br>DNS TCP/UDP 53<br>SSH TCP 22<br>NetBIOS TCP 137,138,139</td>
         <!-- <td rowspan=3>FTP<br>Telnet<br>SMTP<br>HTTP<br>DHCP<br>TFTP<br>SNMP<br>DNS<br>SSH<br>NetBIOS</td>
         <td rowspan=3>TCP 20,21<br>TCP 23<br>TCP 25<br>TCP 80<br>UDP 67,68<br>UDP 69<br>UDP 161,162<br>TCP/UDP 53<br>TCP 22<br>TCP 137,138</td> -->
         <td rowspan=3></td>
         <td rowspan=3></td>
         <td rowspan=3 style="font-weight:bold">Application<br>(응용)</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Presentation(표현)</td>
         <td>부호화, 암호화, 압축, 데이터 포맷 결정</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Session(세션)</td>
         <td>프로그램 간 애플리케이션 연결 설정, 유지, 해지</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Transport(전송)</td>
         <td>응용계층 사이에 논리적인 통로 제공(프로세스 간 통신)</td>
         <td>segment</td>
         <td>TCP, UDP</td>
         <!-- <td></td> -->
         <td>포트 주소</td>
         <td></td>
         <td style="font-weight:bold">Transport<br>(전송)</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Network(네트워크)</td>
         <td>라우팅 목적지까지 데이터 전송, 최적 경로 설정</td>
         <td>packet</td>
         <td>ICMP<br>IP<br>ARP</td>
         <!-- <td></td> -->
         <td>IP주소</td>
         <td>라우터</td>
         <td style="font-weight:bold">Internet<br>(인터넷)</td>
      </tr>
      <tr>
         <td style="font-weight:bold">DataLink(데이터 링크)</td>
         <td>흐름 제어, 에러 제어</td>
         <td>frame</td>
         <td>Ethernet</td>
         <!-- <td></td> -->
         <td>MAC주소</td>
         <td>스위치<br>브릿지</td>
         <td rowspan=2 style="font-weight:bold">Network Access<br>(네트워크 액세스)</td>
      </tr>
      <tr>
         <td style="font-weight:bold">Physical(물리)</td>
         <td>bit 신호의 물리적 전송, 물리적 연결 </td>
         <td>bit</td>
         <td></td>
         <!-- <td></td> -->
         <td></td>
         <td>리피터, 허브</td>
      </tr>
   </table>   
      
   <span style="font-size:18px"><02강.네트워크 모델></span>      
   <span style="font-size:18px">bit(3자) -> frame(5자) -> packet(6자) -> segment(7자)</span>   
   <span style="font-size:18px"> <string>데</string>이<string>터</string> ≒ 이<string>더</string>넷</span>   

1. # 패킷
   네트워크 상에 전달되는 데이터를 통칭하는 말로 네트워크에서 전달하는 데이터의 형식화된 블록   
   패키시은 제어 정보와 사용자 데이터로 이루어지며 사용자 데이터는 페이로드라고도 함   

   데이터 전송 시 - 패킷을 만드는 과정(캡슐화)   

   | 헤더 | 페이로드 | 풋터   
   
   페이로드가 주 전송 데이터가 되고 여기에 헤더나 풋터가 붙는 방식입니다. 주로 헤더가 붙습니다.   
   페이로드에 헤더가 붙으면 그 전체가 새로운 페이로드가 되고 다시 여기에 새로운 헤더가 붙습니다.   
   상위계층(응용계층)에서 점점 하위계층(물리적계층)으로 내려오면서 데이터를 
   점점 추가하고 받을 땐 역순으로 하나씩 해석을 합니다. 상자를 포장하고 그 상자를 다시 포장하고.. 상자 속에 또 상자가 있는 모습과 유사합니다.
   
   ex) | Ethernet | IPv4 | TCP | HTTP |    
   란 패킷이 있을 때   
   1) HTTP란 페이로드에 TCP란 헤더가 붙습니다.   
   2) HTTP, TCP란 페이로드에 IPv4란 헤더가 붙습니다.   
   3) HTTP, TCP, IPv4란 페이로드에 Ethernet이란 헤더가 붙습니다.   
   
   이것을 패킷의 __캡슐화라__ 고 합니다.   

   상위계층을 먼저 캡슐화하고 하위계층을 캡슐화하지 하위 계층을 먼저 갭슐화하지 않습니다.   
   <span style="color:red">4계층 -> 2계층 -> 3계층</span>   
   이런식의 캡슐화는 불가능 합니다.   
