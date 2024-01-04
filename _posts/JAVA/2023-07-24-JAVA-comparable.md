---
layout: single
title: Comparable과 Comparator
categories: JAVA
tag: [comparable, comparator]
---

1. # Comparable과 Comparator 인터페이스
   객체의 정렬을 위해 사용하는 인터페이스입니다. 두 객체를 비교하여 오름차순 또는 내림차순으로 정렬하는데 Comparable에서는 compare과 Comparator에서는 compareTo 메소드를 제공합니다.   

   Comparator - java.util
   ```java
      public interface Comparator{
         int compare(T o1, T o2)
      }
   ```

   Comparable - java.lang   
   ```java
      public interface Compareable{
         int compareTo(T o)
      }
   ```   
   기본정렬(오름차순) 기준으로 구현되어 있습니다.

1. # Comparable과 Comparator 비교
   comparable의 compareTo와 comparator의 compare를 오버라이딩하는 소스입니다.
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