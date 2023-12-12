---
layout: single
title: int와 Integer 변환
categories: JAVA
tag: 
---

1. # int -> Integer
   ```java 
      int int1_1 = 34;
      Integer integer1_1 = new Integer(12); //new Integer이용 : 이 방법은 JDK9버전부터 deprecation되었다. error는 나지 않지만 권장하지 안는 방법이다
      integer1_1 = Integer.valueOf(int1_1); //Integer.valueOf이용
   ```
   new Integer()를 이용한 변환은 JDK9부터 지양하는 방식이 되었습니다. JAVA에서는 valueOf의 사용을 권장하고 있습니다.
1. # Integer -> int
   ```java
      Integer integer1_2 = 76;
      int int1_2 = integer1_2.intValue();
   ```
1. # int[] -> Integer[]
   ```java
      int[] int2_1 = {1,2,3,4};
      Integer[] integerA = Arrays.stream(int2_1).boxed().toArray(Integer[]::new);
   ```
1. # Integer[] -> int[]
   ```java
      Integer[] integer2_2 = {1,2,3,4};
      int[] int2_2 = Arrays.stream(integer2_2).mapToInt(Integer::intValue).toArray(); //--㉠
      int2_2 = Arrays.stream(integer2_2).mapToInt(i->i).toArray(); // --㉡
   ```
   ㉠에선 mapToInt에서 메서드 참조를 사용하였고 ㉡은 람다식을 사용했습니다.