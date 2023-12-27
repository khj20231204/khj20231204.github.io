---
layout: single
title: Stream
categories: JAVA
tag: [stream]
---

1. # Stream이란
   기존의 배열이나 컬렉션을 다루기 위해선 for문을 사용하거나 Iterator를 사용해야 했습니다. 이는 코드가 길어지고 재사용성이 떨어지며 무엇보다 사용법이 각각이라 불편함이 있었습니다.
   ```java
      //선언
      String[] strArr = {"aaa","bbb","ccc","abe"};
		List<String> strList = Arrays.asList(strArr); //Arrays를 List로

      //정렬
      Arrays.sort(strArr); //배열정렬-Arrays이용
		Collections.sort(strList); //List정렬-Collections이용
		
      //출력
		for(String s : strArr) {
			System.out.print(s + " ");
		}

      //List는 iterator이용
      var iter = strList.iterator();
		while(iter.hasNext()) {
			String s = iter.next();
			System.out.print(s);
		}
      //또는 for문으로
		for(String s: strList) {
			System.out.print(s + " ");
		}
		
   ```
   배열은 Arrays.sort()를 이용해서 정렬하고 컬렉션은 Collection.sort()를 이용해서 정렬해야 하며, 컬렉션의 경우 iterator를 사용해야 했습니다.
   이러한 불편함을 줄이고 재사용성을 높이기 위해서 데이터를 자주 다루는 메소드들을 정의하고 데이터 소스를 추상화하여 하나로 묶은 클래스가 Stream입니다.
   ```java
      String[] strArr = {"aaa","bbb","ccc","abe"};
		List<String> strList = Arrays.asList(strArr); //Arrays를 List로

      //배열과 List의 Stream을 선언
		Stream<String> streamArr = Arrays.stream(strArr);
		Stream<String> streamList = strList.stream();

      //정렬과 출력을 한번
      streamArr.sorted().forEach(System.out::println);
		strList.stream().sorted().forEach(System.out::println);
   ```
   sorted()는 요소들을 정렬시키고 forEach()는 각각의 모든 요소에 action을 수행하게 됩니다.
1. # Stream의 특성   
      2. __스트림은 데이터 소스를 변경하지 않습니다.__   
         스트림은 데이터를 읽기만 할 뿐 값을 변경하지 않습니다. 그래서 결과를 컬렉션이나 배열에 담아야합니다.   
         ```java
            List<String> list = streamArr.sorted().collect(Collections.toList()); //배열을 List로
         ```
      2. __스트림은 일회용입니다.__   
         스트림은 한번 사용하면 닫혀서 다시 사용할 수 없다.   
         ```java
            Stream<String> streamArr = Arrays.stream(strArr);
            List<String> list = streamArr.sorted().collect(Collections.toList());
            List<String> list2 = streamArr.sorted().collect(Collections.toList()); //error발생
         ```
         streamArr에 대한 stream을 재생성 해줘야 합니다.   
         ```java
            Stream<String> streamArr = Arrays.stream(strArr);
            List<String> list = streamArr.sorted().collect(Collections.toList());

            streamArr = Arrays.stream(strArr); //재생성
            List<String> list2 = streamArr.sorted().collect(Collections.toList()); 
         ```
      2. __스트림은 작업을 내부 반복으로 처리합니다.__   
         forEach()와 같은 메소드를 사용하게 되면 내부적으로 메소드 안에선 for문 사용하게 됩니다.   
1. # Stream의 연산
   중간 연산과 최종 연산으로 분류할 수 있습니다. 모든 중간 연산의 결과는 스트림으로 반환하기 때문에 연산을 계속 수행할 수 있습니다. 
   반면 최종 연산은 스트림의 요소를 소모하여 연산을 수행하기 때문에 스트림의 일회성으로 인해 한번만 연산이 가능합니다.
      ```java
         String[] strArr = {"aaa","bbb","ccc","abe"};
         Arrays.stream(strArr).distinct().limit(2).sorted().forEach(System.out::println);
      ```
   *stream(strArr).distinct().limit(2).sorted()*까지 중간 연산이 되고 마지막 *forEach*가 최종 연산이 됩니다.
1. # 중간 연산자   
   2. __distinct__   
      중복을 제거합니다.   
   2. <strong>filter(Predicate<T> p)</strong>   
      조건에 안 맞는 요소 제외합니다.   
   2. __limit(long max)__   
      스트림의 일부를 잘라냅니다.   
   2. __skip(long n)__   
      스트림의 일부를 건너뜁니다.   
   2. __sorted()__   
      스트림의 요소를 정렬합니다.   
   2. __변환__   
      mapToDouble(ToDoubleFunction<T> mapper)<br>
      ex)mapToDouble(Integer::doubleValue) Integer를 double로 변환<br>
      mapToInt(ToIntFunction<T> mapper)<br>
      ex)mapToInt(Integer::intValue) Integer를 int로 변환<br>
      mapToLong(ToLongFunction<T> mapper)<br>
      ex)mapToLong(Integer::longValue) Integer를 long로 변환<br>
      <br>
1. # 최종 연산자
   1. <strong>forEach(consumer<? super T> action)</strong>   
      각 요소에 action을 수행합니다.   
   1. __count()__   
      스트림의 요소 개수 반환합니다.   
   1. <strong>Option<T> Max (Comparator<? super T> comparator)</strong>   
      스트림의 최대값 반환합니다.   
   1. <strong>Option<T> Min(Comparator<? super T> comparator)</strong>    
      스트림의 최소값 반환합니다.   
   1. __Object[] toArray()__    
      배열로 변환합니다.   
   1. <strong>collect(Collector<T> collector)</strong>   
      스트림의 요소를 수집합니다.   
   <br>
1. # 컬렉션에서 스트림 생성하기   
   Collection에 stream()이 정의되어 있습니다. Collection의 자손인 List, Set등 Collection으로 구현한 클래스들은 모두 stream()메소드로 스트림을 생성할 수 있습니다
   ```java
      List<Integer> list = new ArrayList<>();
      list.add(3);
      list.add(35);
      list.add(72);

      Stream<Integer> s = list.stream();
      s.forEach(System.out::println); //3 35 7
   ```   
   <br>
1. # 배열에서 스트림 생성하기
   1. __문자열 스트림__   
      Stream<T> Stream.of(T values);   
      Stream<T> Stream.of(T[]);   
      Stream<T> Arrays.stream(T[]);   
      ```java
         Stream<String> strStream1 = Stream.of("a","c" ,"b");
         Stream<String> strStream2 = Stream.of(new String[]{"a","c" ,"b"});
         Stream<String> strStream3 = Arrays.stream(new String[] {"a","c","b"});
         
         strStream1.forEach(t->System.out.println(t)); //acb
         strStream2.forEach(t->System.out.println(t)); //acb
         strStream3.forEach(t->System.out.println(t)); //acb
      ```
   1. __기본형 스트림__   
      IntStream IntStream.of(int.. values);   
      IntStream IntStream.of(int[]);   
      IntStream Arrays.stream(int[]);   
      ```java
         IntStream is1 = IntStream.of(6,4,2,1);
         IntStream is2 = IntStream.of(new int[] {6,4,2,1});
         IntStream is3 = Arrays.stream(new int[] {6,4,2,1});
         
         is1.forEach(t->System.out.println(t)); //6 4 2 1
         is2.forEach(t->System.out.println(t)); //6 4 2 1
         is3.forEach(t->System.out.println(t)); //6 4 2 1
      ```
      이 외에도 long,double 타입의 LongStream와 DoubleStream이 있습니다.




   
   