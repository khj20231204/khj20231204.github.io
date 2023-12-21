---
layout: single
title: HashMap
categories: JAVA
tag: [HashMap]
---

1. # map활용 소스
   ```java
   class MyData{
      int v;

      public MyData(int v) {
        this.v = v;
      }

      public String toString() {
        return "["+v+"]";
      }

      @Override
      public int hashCode() {
        return Objects.hash(v);
      }

      @Override
      public boolean equals(Object obj) {
        if (this == obj)
            return true;
        if (obj == null)
            return false;
        if (getClass() != obj.getClass())
            return false;
        MyData other = (MyData) obj;
        return v == other.v;
      }
   }

   public class HashTableExam {
   //HashMap : not synch
   //Hashtable : synch
   //concurrentHashMap : synch + high concurrency

   public static void main(String args[]) {
      //Map<String,Integer> map = new HashMap<String, Integer>();
      Map<String, Integer> map = new HashMap<>();
     /* put(key, value)-key가 있으면 value를 덮어쓰고 없으면 새로 삽입 */
     map.put("a", 5);
     map.put("b", 3);
     map.put("c", 8);
     map.put("c", 11); //키"c"가 있으면 11을 덮어쓰고 없으면 새로 삽입힌다.
     System.out.println(map.get("d")); //null

     /* containsKey(key)-key가 있으면 true, 없으면 false 반환 */
     System.out.println(map.containsKey("a"));

     /* containsValue(value)-value가 있으면 true, 없으면 false 반환 */
     System.out.println(map.containsValue(5));
 
     /*
     getOrDefault(key,defaultValue)-key가 있으면 value출력, key가 없으면 defaultValue 출력,
     없는 key값이 defaultValue와 함께 map에 입력되진 않는다, 키의 존재 유무를 확인 후 값을 출력만 한다
     */
     System.out.println(map.getOrDefault("a", 21)); //5
     System.out.println(map.getOrDefault("d", 21)); //21
     System.out.println(map.get("d")); //null

     /*
     putIfAbsent(key,value)-Key가 없으면 value를 입력, 있으면 기존 value출력
     없는 key값이 value와 함께 map에 입력된다. 키가 있으면 기존 value반환, 없어서 값을 입력하게 되면 null반환
     */
     System.out.println("c:"+map.putIfAbsent("b", 11)); //3
     System.out.println(map.get("b")); //3
     System.out.println(map.putIfAbsent("d", 11)); //null
     System.out.println(map.get("d")); //11

     /*
     remove(key)-성공하면 value반환, 실패하면 null반환
     remove(key, value)-성공하면 true반환, 실패하면 false반환
     */
     System.out.println("remove result:" + map.remove("e")); //null
     System.out.println("remove result:" + map.remove("b", 5)); //false 키와 값이 일치해야 삭제가능, 삭제 성공이면 true를, 실패면 false를 리턴한다.

     /*
     repalce(key, value)-key가 있으면 value로 교체 후 기존 value반환, 없으면 null반환
     put(key,value)은 key가 없으면 value를 새로 삽입하지만 repclae는 교체만 가능
     */
     System.out.println(map.replace("c", 15)); //11
     System.out.println(map.replace("e", 15)); //null

     /*
     replace(key, oldValue, newValue) - key값의 value가 oldValue와 일치해야만 newValue삽입
     성공하면 true반환, 실패하면 false반환
     */
     System.out.println(map.replace("c", 7, 9)); //false

     System.out.println(map.keySet()); //map에서 키만 뽑아낸다. [a, b, c, d]
     System.out.println(map.values()); //map에서 값만 뽑아낸다. [5, 3, 15, 11]


      Map<MyData, Integer> map2 = new HashMap<MyData, Integer>();
      MyData mydata = new MyData(8);
      map2.put(new MyData(5), 7);
      map2.put(mydata, 92);
      map2.put(new MyData(3), 3);
      //mydata.toString();
      System.out.println("mydata:" + map2.get(mydata));
      method1(map2);
   }

   static void method1(Map<MyData, Integer> map) {
      System.out.println(map);
      System.out.println(map.get(new MyData(5)));
      /*
      map.get(new MyData(5)); 에서 new 연산자로 새로운 객체를 생성해도 값을 가져오는 이유
      Map은 키값을 ha hashing하면서sh값이 bucket의 인덱스로 들어간다
      hashing : 키 -> hash function -> hash출력 -> bucket에 인덱스로 hash를 입력
      hashing한다 : 키를 hash값으로 bucket에 넣는다
      hashCode()를 오버라이딩했기 때문에 new MyData(5)를 하면 '5'에 해당하는 hash값이 출력되고 이 값이 키가 되어 기존에 있는 데이터를 가져온다
      */
      }
   }
   ```
1. # list와 Map의 데이터 중복
   list는 중복 저장
   ```java
      int a = 5;
      List<Integer> list = new ArrayList<>();
      list.add(a);
      list.add(a);
      list.add(a);
      System.out.println(list); //[5,5,5]
   ```   
   a를 3번 입력 후 전부 저장   
   <br>
   map은 키가 중복 될 경우 가장 마지막 입력 키값이 저장   
   ```java
      int a = 5;
      Map<Integer, Integer> map = new HashMap<>();
      map.put(a,1);
      map.put(a,1);
      map.put(a,2);
      System.out.println(map); //{5=2}
   ```   
   키값5에 해당하는 값으로 가장 마지막 2가 저장   
1. # List와 Map의 데이터가 없는 경우 반환값
    list.contains(element)
   ```java
      /* contains(값)-해당 값이 있으면true 없으면false, 반환값:boolean */
      System.out.println(list.contains(52));//true
      System.out.println(list.contains(59));//false
   ```
   element가 있는 경우  true, 없으면 false 반환   
   ```java
      Map<Integer, Integer> map = new HashMap<>();
      map.put(1,1);
      System.out.println(map.get(2)); //null 반환

      if(map.get(2) == null){
         System.out.println("null");
      }
   ```
   키가 없는 경우 null반환