---
layout: single
title: JPA - 값 타입 분류류
categories: JPA
tab: []
---

1. # 엔티티 타입
   @Entity로 정의하는 객체   
   데이터가 변해도 식별자로 지속해서 추적 가능   
   예)회원 에티티의 키나 나이 갓ㅂ을 변경해도 식별자로 인식 가능   

1. # 값 타입
   int, Integer, String처럼 단순히 값으로 사용하는 자바 기본 타입이나 객체   
   식별자가 없고 값만 있으므로 변경시 추적 불가   
   예)숫자 100을 200으로 변경하면 완전히 다른 값으로 대체   

1. # 기본값 타입
   자바 기본 타입(int, double)   
   래퍼 클래스(Integer, Long)   
   String

1. # 임테디드 타입(embedded type, 복합 값 타입)

1. # 컬렉션 값 타입(collection value type)