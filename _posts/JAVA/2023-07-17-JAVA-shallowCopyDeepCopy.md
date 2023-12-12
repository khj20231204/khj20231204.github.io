---
layout: single
title: 얕은 복사와 깊은 복사
categories: JAVA
tag: [얕은 복사, 깊은 복사]
---

1. # 얕은 복사(Shallow Copy) - 주소 복사
   얕은 복사는 복사된 변수와 원본 변수가 같은 객체를 가리키는 경우입니다. 이 경우, 주소를 복사하므로 두 변수는 동일한 객체를 가리키게 됩니다. 따라서, __한 변수의 값이 변경되면 다른 변수에도 영향을 줍니다__.
   ```java
      String original = “Hello”;
      String copy = original;
      System.out.println(copy == original); // true
   ```
1. # 깊은 복사(Deep Copy) - 값만 복사
   깊은 복사는 복사된 변수와 원본 변수가 서로 다른 객체를 가리키는 경우입니다. 이 경우, 값을 복사하므로 두 변수는 독립적인 객체를 가리키게 됩니다. 따라서, __한 변수의 값이 변경되어도 다른 변수에는 영향을 주지 않습니다__.
   ```java
      String original = “Hello”;
      String copy = new String(original);
      System.out.println(copy == original); // false
   ```
   깊은 복사를 하기 위해서는 String 클래스의 copy 메소드를 사용하거나, 직접 새로운 String 객체를 생성하여 값을 복사해야 합니다.

