---
layout: single
title: JPA - 기본 환경
categories: JPA
tab: []
---

1. # 설명
   1)@Table 어노테이션 생략 시 클래스명이 테이블 명   
   @Table(name = "Test")    
   => @Table 어노테이션 생략 시 클래스명을 기반으로 동일한 이름으로 테이블 생성됨   

   2)기본 생성자는 필수   
   @NoArgsConstructor(access = AccessLevel.PROTECTED) //엔티티 클래스 정의 시 기본 생성자 필수   

   