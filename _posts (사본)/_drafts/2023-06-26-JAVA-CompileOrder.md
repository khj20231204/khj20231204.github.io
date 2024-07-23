---
layout: single
title: JAVA Compile순서
---

# 자바 컴파일 순서
개발자가 작성한 소스코드는 .java란 확장자를 가집니다. ➔  javac(자바 컴파일러)가 .class란 확장자를 가진 파일로 컴파일 합니다. 이파일은 JVM(자바 가상 머신)이 해석하는 파일입니다. 


public static void main(String[] args){

      Map<String, Integer> map = new HashMap<>();

      map.put("a",12);
      map.put("b",43);

      //키만 가져오기
      System.out.println(map.keySet());

      //밸류만 가져오기

      //키값 있는지 확인

      //밸류값 있는 지 확인
   }