---
layout: single
title: Iterator
categories: JAVA
tag: []
---

1. # Iterator
   자바에서 제공하는 컬렉션 프레임워크에 저장된 데이터를 가져오기 위해서 만들어진 인터페이스로 iterator()메소드를 통해 데이터에 접근 합니다.   

   set과 Map에서는 인덱스가 없기 때문에 iterator인터페이스를 구현한 iterator() 메소드로 데이터를 가져옵니다.   

   boolean hasNext() : 가져올 element가 있으면 true, 없으면 false   
   next() : 하나의 element를 가져옵니다.   
   void remove() : element를 제거   

1. # Iterator 예
   Set으로 만든 간단한 예제   

   ```java
      Set<String> set = new HashSet<>();
      set.add("c");
      set.add("f");
      set.add("a");
      set.add("b");

      Iterator iterator = set.iterator(); //iterator생성
      while ((iterator.hasNext())) {  //다음 데이터 확인
         Object o = iterator.next();  //Objec로 요소 반환
         System.out.print(o.toString());
      }
   ```   

   객체.iterator() 메소드로 iterator를 생성합니다.   
   iterator.hasNext() 다음 요소가 있는지 확인 후 있으면 true를, 없으면 false를 반환합니다.   
   해당 요소는 next()메소드를 통해 가져옵니다.   

1. # Iterator 주의할 점

   - ## hasNext() 사용 시
   Iterator는 컬렉션 트랙에서 현재 위치를 나타내는 cursor가 있는데 hasNext를 통해 true가 반환되면 cursor가 다음 요소로 하나씩 이동하게 됩니다. 이후 마지막에 도달하면 다시 원래 값으로 원상복구가 되는 것이 아니라 끝 지점에 머물러 있기 때문에 한번 데이터를 읽고싶다면 iterator()를 새로 생성해 줘야 합니다.   
   ```java
      Iterator iterator = set.iterator();  //← 여기서 iterator생성   
      while ((iterator.hasNext())) {  //← 마지막에 도달
         Object o = iterator.next();
         System.out.print(o.toString());
      }
      
      while ((iterator.hasNext())) {  //← false로 출력되어서 루프 실행 안 됨
         Object o = iterator.next();
         System.out.print(o.toString());
      }
   ```   
   hasNext()로 마지막에 도달한 후 다시 호출해도 현재 커서는 요소의 마지막을 가리키고 있기 때문에 밑에 while문은 실행되지 않습니다. 이 경우 다시 iterator()를 생성해 줘야 합니다.   
   ```java
      Iterator iterator = set.iterator();  
      while ((iterator.hasNext())) {  
         Object o = iterator.next();
         System.out.print(o.toString());
      }

      iterator = set.iterator();  // ← 다시 생성
      while ((iterator.hasNext())) {  
         Object o = iterator.next();
         System.out.print(o.toString());
      }
   ```   

   - ## remove() 사용 시
   Iterator.remove()를 이용해서 요소를 삭제 시 원본 컬렉션의 데이터가 삭제됩니다. iterator를 생성했고 생성한 객체의 요소를 삭제했다고 iterator에서만 삭제되고 원본은 그대로 있는 것이 아니라 원본이 삭제가 됩니다. 참조 값으로 iterator를 생성하기 때문에 원본 컬렉션의 요소들이 삭제가 됩니다.   
   ```java
      Set<String> set = new HashSet<>();
      set.add("c");
      set.add("f");
      set.add("a");
      set.add("b");

      Iterator iterator = set.iterator();
      while ((iterator.hasNext())) {
         Object o = iterator.next();
         iterator.remove();  // ← ㉠
      }
   ```   
   ㉠에서 remove메소드를 실행 시 set 컬렉션의 "c,f,a,b" 데이터가 삭제 됩니다.   
   ```java
      Set<String> set = new HashSet<>();
      set.add("c");
      set.add("f");
      set.add("a");
      set.add("b");

      Iterator iterator = set.iterator();
      while ((iterator.hasNext())) {
         Object o = iterator.next();
         iterator.remove();
      }

      System.out.println("-----------");

      iterator = set.iterator();
      while ((iterator.hasNext())) {
         Object o = iterator.next();
         System.out.print(o.toString());
      }

      출력 결과 :
      -----------
   ```   
   set 객체에 남아있는 값이 없습니다.   
