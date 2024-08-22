---
layout: single
title: 메소드 참조
categories: JAVA
tag: 
---

1. # 메서드 참조
   람다식이 하나의 메소드만 호출하는 경우 메서드 참조 방식으로 람다식을 간략히 나타낼 수 있습니다.   

      ```java
         Integer wrapper(String s){
            return Integer.parseInt(s);
         }
      ```   
   다음과 같은 함수가 있습니다. String 타입의 문자열 s를 입력받아서 Integer.parseInt(s)를 이용해서 숫자로 변환 후 반환 함수입니다.   

   이것을 간략히 하면   

      ```java
         Function<String, Integer> f = (String s) => Integer.parseInt(s);
      ```   
   다음과 같은 람다식이 됩니다. s가 String타입인 것은 parseInt함수를 보면 알 수 있고, String과 Integer인 인자를 2개 받아서 String을 받아서 Integer로 반환한다는 것은 왼쪽 제네릭 타입을 보면 알 수 있습니다. 그렇기 때문에 parseInt안에 매개변수 값을 생략하고 String s를 생략하면   

      ```java
         Function<String, Integer> f = Integer::parseInt;
      ```   
   와 같이 나타낼 수 있습니다.   

   *Function<A,B> : 가장 마지막 B는 함수의 리턴 타입, A는 매개변수 타입   
   Function<A,B,C> : 가장 마지막 C는 함수의 리턴 타입, A,B는 매개변수 타입   

   마찬가지로   

      ```java
         BiFunction<String, String, Boolean> f = (s1,s2) => s1.equal(s2);   
      ```   
   를 다음과 같이 변경할 수 있습니다.   
      ```java
         BiFunction<String, String, Boolean> f = String::equal;
      ```   
   equal안에 매개변수를 생략하고 (s1,s2)를 생략하면 equal만 남는데 equal이 어디에 있는 메서드인지 정의하기 위해서 String을 써줍니다.   

   생략할 수 있는 것들을 생략하고 나면 parseInt와 equal인 메소드만 남기 때문에 메소드 참조라고 합니다. 그리고 메소드를 구별해주기 위해 앞에 클래스나 객체를 적어줍니다.   

      ```
         A::B
      ```   
   A : 클래스나 객체   
   B : A에 속한 메서드   

   가 됩니다.
 
1. # 생성자 메서드 참조
   생성자를 호출하는 람다식도 메서드 참조로 변환할 수 있습니다.   

      ```java
         Supplier<MyClass> s = () => new MyClass(); //람다식
         
         Supplier<MyClass> s = MyClass::new        //메소드 참조형
      ```    
   MyClass myclass = new MyClass(); 처럼 매개변수가 없는 기본생성자를 메소드 참조형으로 변환한 것입니다.   

   매개변수가 있는 생성자   

      ```java
         Function<Integer, MyClass> f = (i) => new MyClass(i);
      ```   
   `<Integer, MyClass>`란 입력 타입은 Integer, 반환 타입은 MyCass클래스의 객체입니다. Integer타입의 i를 입력 받아서 new MyClass인 MyClass 객체를 반환합니다. 이를 메소드 참조형으로 변환하면   
   
      ```java
         Function<Integer, MyClass> f = MyClass::new
      ```  
   다음과 같이 나타낼 수 있습니다.   

1. # 배열의 메서드 참조
   배열을 생성할 때 메소드 참조입니다.   

      ```java
         Function<Integer, int[]> f = x => new int[x];   //람다식
         Function<Integer, int[]> f = int[]::new;        //메서드 참조
      ```   

1. # forEach에서 메서드 참조

      ```java
         mycollection.sroted().forEach(System.out::println);
      ```   
   mycollection은 List, Set, Map인 컬렉션이나 배열이 될 수 있습니다.   
   System.out이란 클래스 안에 있는 println이란 메서드를 mycollection에 있는 값들을 하나씩 출력하게 됩니다.   

      ```java
         List<Integer> intVar = new ArrayList<>();
         int[] intArr = new int[5];
         
         for(int i=0 ; i<5 ; i++) {
            int r = (int)(Math.random()*10);
            intVar.add(r);
            intArr[i] = r;
         }
         
         intVar.stream().forEach(System.out::println);
         
         Arrays.stream(intArr).forEach(System.out::println);
      ```   

   객체에 있는 메소드도 사용할 수 있습니다.   
      ```java
         int[] intArr = new int[5];
         for(int i=0 ; i<5 ; i++) {
            int r = (int)(Math.random()*10);
            intArr[i] = r;
         }
         
         Queue<Integer> queue = new LinkedList<>();
         Arrays.stream(intArr).forEach(queue::offer); //queue::offer
      ```   
   intArr에 있는 배열 값을 forEach로 루프를 돌면서 queue객체의 offer 메소드를 사용하여 queue에 입력하게 됩니다.   
