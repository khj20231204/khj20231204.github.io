---
layout: single
title: Comparable과 Comparator
categories: JAVA
tag: [comparable, comparator]
---

1. # Comparable과 Comparator 인터페이스
   객체의 정렬을 위해 사용하는 인터페이스입니다. 두 객체를 비교하여 오름차순 또는 내림차순으로 정렬하는데 Comparable 인터페이스에서는 compare 추상 메소드를, Comparator 인터페이스에서는 compareTo 추상 메소드를 제공합니다. 실제 사용시엔 추상 메소드를 구현해줘야 합니다.   

   __Comparator__ - java.util
   ```java
      public interface Comparator{
         int compare(T o1, T o2)
      }
   ```   
   o1과 o2를 비교합니다.   
   compare의 결과로 양수, 0, 음수를 리턴하는데    

   | 부호  |   결과 값   |
   |:-----:|:----------:|
   | 양수  | 왼쪽이 크다 |
   |   0   |    같다    |   
   | 음수  |오른쪽이 크다|     

   와 같은 결과를 가져옵니다.   

   __Comparable__ - java.lang   
   ```java
      public interface Compareable{
         int compareTo(T o)
      }
   ```   
   자기 자신과 o를 비교합니다.
   기본정렬(오름차순) 기준으로 구현되어 있습니다.
 
1. # String에서 Sort
   Stirng클래스에서 Sort시 이용되는 기본 비교 인터페이스는 compareTo 추상 메소드를 이용한 정렬로 오름차순(사전순)입니다.   
   ```java              
      Arrays.sort(strArry, new Decending());

      class Decending implements Comparator{
         public int compare(Object o1, Object o2){
            if(o1 instanceof Comparable && o2 instanceof Comparable){
               Comparable c1 = (Comparable)o1;
               Comparable c2 = (Comparable)o2;

               return c1.compareTo(c2) * (-1)
            }
         }
      }
   ```   
   Arrays의 sort메소드 정의는 sort(T[] a, Comparator<? super T> c) 다음과 같습니다. 두 번째 인자로 Comparator 인터페이스를 넣으면 Comparator의 추상 메소드 compare를 재정의한 부분이 실행됩니다. String과 rapper클래스들은 전부 Comparable 인터페이스를 상속 받았기 때문에 형변환이 가능합니다. 따라서 Comparable c1 = (Comparable)o1; 이런 변환이 가능합니다.   
   c1.compareTo(c2) * (-1) : compareTo로 나온 결과에 -1를 곱하므로써 오름차순이 아니라 내림차순으로 정렬되게 됩니다.   

1. # Comparable과 Comparator 비교
   comparable의 compareTo와 comparator의 compare를 오버라이딩합니다.   
   ```java
      import java.util.Comparator;

      public class ComparableComparator implements Comparable<ComparableComparator>, Comparator<ComparableComparator>{

         int age;
         String name;
         
         public ComparableComparator(int age, String name) {
            this.age = age;
            this.name = name;
            // TODO Auto-generated constructor stub
         }
         
         public static void ComparableComparatorFunc() {
            /*
            Comparable - compareTo(Object o) : compa"able" compare"To" 접미:able, 접미:to
            자기 자신과 Object를 비교
            lang패키지에 있기 때문에 import가 필요없다
          
            Comparator - compare(Object o1, Object o2)
            Object o1과 Object o2를 비교
            utile패키지에 있기 때문에 import를 해야한다.
            */
            
            //Comparator<T>
            //Comparable<T>
         }

         @Override //Comparable
         public int compareTo(ComparableComparator o) {
            // TODO Auto-generated method stub
            int chk = 0;
            if((this.age - o.age) == 0 ) {
               if(this.name.equals(o.name)) {
                  chk = 1;
               }
            }
            
            return chk;
         }

         @Override //Comparator
         public int compare(ComparableComparator o1, ComparableComparator o2) {
            // TODO Auto-generated method stub
            int chk = 0;
            if((o1.age - o2.age) == 0 ) {
               if(o1.name.equals(o2.name)) {
                  chk = 1;
               }
            }
            
            return chk;
         }
      }
   ```

