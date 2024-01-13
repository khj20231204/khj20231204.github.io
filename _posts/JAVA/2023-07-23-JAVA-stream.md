---
layout: single
title: Stream
categories: JAVA
tag: [stream]
---

1. # Stream 이전에 배열과 컬렉션의 사용
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

1. # Stream이란
   기존의 배열이나 컬렉션과 같은 데이터를 다루기 위해선 for문을 사용하거나 Iterator를 사용해야 했습니다. 이는 코드가 길어지고 재사용성이 떨어지며 무엇보다 사용법이 각각이라 불편함이 있었습니다. 따라서 이들을 다루기 위한 일관된 표준 방법을 제공하게 되는데 그것이 스트림입니다. 컬렉션(list, set, map), 배열, 람다식으로부터 스트림을 생성합니다.   
   연산은 스트림 생성 → 중간 연산(n번) → 최종 연산(1번) 순서대로 수행이됩니다.   
   중간 연산 - 연산결과가 스트림이기 때문에 반복 적용가능   
   최종 연산 - 연산결과가 스트림이 아닌 연산으로 __한번만 적용__   
   <span style="color:red">→ 최종 연산 이후 다시 사용하기 위해서 스트림 새로 생성</span>   

   1) 스트림 생성 예   
   ```java
      //list stream
      List<Integer> list = Arrays.asList(1,2,3,4,5);
      Stream<Integer> listStream = list.stream();

      //array stream
      Stream<String> strStream = Stream.of(new String[]{"a","b","c"});

      //lamda stream
      Stream<Integer> evenStream = Stream.iterate(0, n->n+2);
      Stream<Double> randomStream = Stream.generate(Math::random);
   ```   
   Collection들은 전부 stream()메소드를 가지고 있습니다.   
   배열은 Stream.of, 람다식들은 Stream.iterate, Stream.generate와 같은 메소드를 이용해 스트림생성을 합니다.   

   2) 중간 연산 예   
   중간 연산은 결과값이 스트림이기 때문에 이후 연산에서도 스트림 연산이 가능하기 때문에 반복 사용 가능합니다.   
   ```java
      Stream<String> strStream = Stream.of(new String[]{"ef","ab","eg","ab","da","de"});
      strStream.limit(4).sorted().distinct().forEach(System.out::println); //ab ef eg

      System.out.println("----- new stream ----");

      Stream<String> strStream2 = Stream.of(new String[]{"ef","ab","eg","ab","da","de"});
      strStream2.distinct().limit(4).sorted().forEach(System.out::println); //ab da ef eg
   ```   
   중간연산 시 순서가 달라도 연산은 되지만 결과가 같지는 않습니다.   
   첫번째 예는 4개로 제한 하고 정렬 후 중복을 제거 했기 때문에 결과가 "ab ef eg" 3개의 문자열 출력되지만, 두번째 예는 중복을 먼저 제거 후 4개로 제한했기 때문에 결과가 "ab da ef eg" 4개의 문자열이 출력됩니다.   
   연속적인 연산의 흐름을 다음과 같이 하나씩 실행 할 수 있습니다.   
   ```java
      String[] strArray = new String[]{"ef","ab","eg","ab","da","de"}; //배열 생성
        Stream<String> strStream3 = Stream.of(strArray);  //스트림 생성
        Stream<String> disStream = strStream3.distinct();  //distinct 적용
        Stream<String> limStream = disStream.limit(4); //limit 적용
        Stream<String> sortStream = limStream.sorted(); //sort 적용
        sortStream.forEach(System.out::println); //최종 연산
   ```   

1. # 특징
   1) 스트림은 원본 데이터를 읽기만 할 뿐 변경하지 않습니다.   
   원본으로부터 생성된 스트림으로 작업을 하기 때문에 원본은 변함이 없습니다.   
   ```java
      List<String> list = streamArr.sorted().collect(Collections.toList()); //배열을 List로
   ```

   2) 일회용입니다.   
   생성한 스트림으로 최종연산을 한번 수행하고 나면 해당 스트림을 소모하기 때문에 Iterator처럼 다시 생성을 해야합니다. 닫힌 스트림을 사용하면 "stream has already been operated upon or closed" 다음과 같은 에러가 발생합니다.   
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

   3) 지연된 연산
   스트림은 중간 연산을 하나씩 실행하는 것이 아니라 최종 연산이 수행되어서야 전체 요소들의 중간 연산을 포함해 한번에 최종 연산까지 수행을 합니다. 따라서 최종 연산을 수행하기 전까지 중간 연산은 선언만 할 뿐 실행되지는 않기 때문에 중간 연산을 지연된 연산이라 합니다.   
   ```java
      IntStream intStream = new Random().ints(1,46);
      intStream.distinct().limit(5).forEach(System.out::println); //37,16,34,5,14
   ```
   Random().ints()메소드는 무한 스트림입니다.   
   "IntStream intStream = new Random().ints(1,46)" 한 줄만 따로 실행이 된다면 1~46까지의 난수가 계속 출력이 될 것입니다. 하지만 바로 뒤에 intStream.distinct().limit(5) 이런 중간 연산이 가능한 이유는 바로 연산을 수행하지 않고 지연된 연산을 하기 때문에 가능합니다.   

   4) 작업을 내부 반복으로 처리   
   Stream.forEach(System.out::println);   
   다음과 같은 forEach문을 스트림은 내부적으로 임의의 메소드 안에 넣어서 실행합니다.   
   ```java
      stream.forEach(System.out::println);

      void forEach(Consumer<? super T> action){
         Object.requireNonNull(action);

         for(T t : src) action.accept(T);  //← for 반복문을 내부 메소드 안에 넣어서 실해이
      }
   ```   
   내부 반복적으로 처리하면 속도는 느려지지만 소스 코드가 간결해지는 장점이 있기 때문에 속도 보단 가독성을 위해서 코드가 간결해지는 부분으로 처리   

   5) 스트림은 기본형을 제공합니다.   
   Stream<T>로 선언시 제네릭 타입 T에 들어가는 타입은 참조형이여야 합니다. 숫자로 배열은 선언시 {}안에 타입은 int가 됩니다. 그렇기 때문에 int를 Integer로 바꾸고, 다시 Integer를 Int로 바꾸는 박싱과 언박싱을 해야하는데, 이런 불편함을 없애기 위해 스트림 자체에서 기본형 타입인 IntStream, LongStream, DoubleStream을 제공합니다. 
   *스트림명 앞이 대문자 Long, Double라고해서 래퍼클래스를 지원하는 스트림이 아님

1. # 컬렉션에서 스트림 생성하기   
   Collection에 stream()이 정의되어 있습니다. Collection의 자손인 List, Set등 Collection으로 구현한 클래스들은 모두 stream()메소드로 스트림을 생성할 수 있습니다   
   ```java
      Interface Collection<E> {
         ...
         Stream<E> stream()
         ...
      }
   ```   
   Collection 인터페이스 안에 추상메소드로 stream이 선언되어 있습니다.   
   따라서 List, Set, Map의 객체를 생성 후 객체.stream()으로 접근 합니다.   

   ```java
      List<Integer> list = new ArrayList<>();
      list.add(3);
      list.add(35);
      list.add(72);

      Stream<Integer> s = list.stream();  //list를 스트림으로 변환
      s.forEach(System.out::println); //3 35 7
   ```   
   Collection의 출력은 forEach를 사용합니다. forEach는 최종 연산에 속합니다.   

1. # 배열에서 스트림 생성하기
   - Arrays클래스에 선언되어 있는 stream 메소드로 스트림 생성   
   ```java
      public class Arrays extends Object{
         static DoubleStream	stream(double[] array){ ... }
         //Returns a sequential DoubleStream with the specified array as its source.
         static DoubleStream	stream(double[] array, int startInclusive, int endExclusive){ ... }
         //Returns a sequential DoubleStream with the specified range of the specified array as its source.
         static IntStream	stream(int[] array){ ... }
         //Returns a sequential IntStream with the specified array as its source.
         static IntStream	stream(int[] array, int startInclusive, int endExclusive){ ... }
         //Returns a sequential IntStream with the specified range of the specified array as its source.
         static LongStream	stream(long[] array){ ... }
         //Returns a sequential LongStream with the specified array as its source.
         static LongStream	stream(long[] array, int startInclusive, int endExclusive){ ... }
         //Returns a sequential LongStream with the specified range of the specified array as its source.
         static <T> Stream<T>	stream(T[] array){ ... }
         //Returns a sequential Stream with the specified array as its source.
         static <T> Stream<T>	stream(T[] array, int startInclusive, int endExclusive){ ... }
         //Returns a sequential Stream with the specified range of the specified array as its source.
      }
   ```   
   Arrays클래스 안에 기본형 타입에 맞춰 static으로 오버로딩 된 상태로 선언되어 있습니다.   
   따라서 Arrays.stream(배열명)으로 접근하게 됩니다.   
   startInclusive와 endExclusive는 배열의 범위를 선택합니다. 배열 중 일부분만을 선택하고 싶을 때 사용합니다.   

   - of 메소드로 스트림 생성
   Arrays클래스 뿐만 아니라 Stream 인터페이스에도 배열을 클래스로 변환해 주는 of 추상 메소드가 존재합니다.   
   Stream인터페이스에 static으로 선언되어 있는 of메소드   
   T값엔 객체가 들어가게 됩니다.   
   ```java
      Interface Stream<T>{
         static <T> Stream<T> of(T... values)
         //Returns a sequential ordered stream whose elements are the specified values.
         static <T> Stream<T> of(T t)
         //Returns a sequential Stream containing a single element
      }
   ```   
   static이기 때문에 Stream.of()로 바로 접근하게 됩니다.   
   기본형 인터페이스로 정의되어진 스트림입니다.   
   ```java
      public interface IntStream extends BaseStream<Integer,IntStream>{
         ...
         static IntStream of(int... values)
         //Returns a sequential ordered stream whose elements are the specified values.
         static IntStream of(int t)
         //Returns a sequential IntStream containing a single element.
         ...
      }
 
      public interface LongStream extends BaseStream<Long,LongStream>{
         ...
         static LongStream of(long... values)
         //Returns a sequential ordered stream whose elements are the specified values.
         static LongStream of(long t)
         //Returns a sequential LongStream containing a single element.
         ...
      }

      public interface DoubleStream extends BaseStream<Double,DoubleStream>{
         ...
         static DoubleStream of(double... values)
         //Returns a sequential ordered stream whose elements are the specified values.
         static DoubleStream of(double t)
         //Returns a sequential DoubleStream containing a single element.
         ...
      }
   ```   
   int, long, double로 선언되어 있습니다.   

1. # 사용 예
   - 객체 배열로 스트림 생성   
   ```java
      Stream<String> strStream4 = Stream.of("a","c" ,"b");  //of 사용
      Stream<String> strStream5 = Stream.of(new String[]{"a","c" ,"b"});  //of 사용
      Stream<String> strStream6 = Arrays.stream(new String[] {"a","c","b"});  //Arrays.stream 사용

      strStream4.forEach(t->System.out.println(t)); //acb
      strStream5.forEach(t->System.out.println(t)); //acb
      strStream6.forEach(t->System.out.println(t)); //acb

      Stream<Integer> integerStream = Stream.of(1,2,3,4);  //of 사용
      Stream<Integer> integerStream = Arrays.stream(new Integer[]{1,2,3,4});  //Arrays.stream 사용
      integerStream.forEach(System.out::println);  //1,2,3,4
   ```   
   Stream<T> T의 타입으로 참조형(String, Integer, Float,..)이 오게 됩니다.   

   - 기본형 배열로 스트림 생성
   ```java
      IntStream is1 = IntStream.of(6,4,2,1);  //of 사용
      IntStream is2 = IntStream.of(new int[] {6,4,2,1});  //of 사용
      IntStream is3 = Arrays.stream(new int[] {6,4,2,1});  //Arrays.stream 사용
      
      is1.forEach(t->System.out.println(t)); //6 4 2 1
      is2.forEach(t->System.out.println(t)); //6 4 2 1
      is3.forEach(t->System.out.println(t)); //6 4 2 1
   ```
   이 외에도 long,double 타입의 LongStream와 DoubleStream이 있습니다.

1. # 람다식으로 스트림 생성
   람다식을 매개변수로 받아서 연산을 수행하는 iterate()와 generate() 메소드가 있습니다.   
   ```java
   public interface Stream<T> extends BaseStream<T,Stream<T>>{
      static <T> Stream<T>	iterate(T seed, UnaryOperator<T> f)
      //Returns an infinite sequential ordered Stream produced by iterative application of a function f to an initial element seed, producing a Stream consisting of seed, f(seed), f(f(seed)), etc.
      static <T> Stream<T>	generate(Supplier<T> s)
      //Returns an infinite sequential unordered stream where each element is generated by the provided Supplier.
   }
   ```   
   iterate와 generate는 모두 무한 스트림입니다. iterate는 이전 요소에 종속적이며, generate는 이전 요소에 독립적입니다.   

   - iterate() 사용 예
   ```java
      Stream<Integer> evenStream = Stream.iterate(0, n->n+2);
   ```   
   초기 값인 씨드 값은 0이 되고, 0+2=2, 2+2=4, 4+2=6,.. 이 됩니다.   

   - generate() 사용 예
   ```java
      Stream<Integer> randomStream = Stream.generate(Math::random);
   ```   
   generate는 초기 값인 씨드 값을 사용하지 않습니다.   

1. # 중간 연산자
   자르기 - skip(), limit()   
   걸러내기 - filter(), distinct()   
   정렬 - sorted()   
   변환 - map() : 원하는 필드만 뽑아내거나 특정 형태로 변환      
   예)   
   ```java
      스트림명.map(s->s.subsdtring(s.indexOfl('.')+1))
      스트림명.map(String::toUpperCase)
   ```   
   기본타입변환 - mapToInt(),mapToLong(),mapToDouble()   
   예)
   ```java
      Stream<String> → IntStream 으로 변환 : mapToInt(Integer::parseInt)
      Stream<Integer> → IntStream 으로 변환 : mapToInt(Integer::intValue)
   ```
   조회 - peek()
   


   





                                        
   



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

   
   