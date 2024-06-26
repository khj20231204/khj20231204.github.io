---
layout: single
title: stack과 queue
categories: CODINGTEST
tag: [stack, queue]
---

1. # Stack과 queue
   set은 list라는 선형자료구조에서 입력 시 중복을 제거하는 알고리즘이 추가 된 프레임워크입니다. 입력 시 규칙을 정한 자료구조가 set이라면 출력시 조건을 입력한 자료구조가 stack과 queue입니다. stack과 queue도 선형자료구조인데 값을 꺼낼 때 꺼내는 규칙이 stack과 queue 각각 다르게 적용되었습니다.   

   stack-뒤에서부터 꺼낸다(가장 나중에 들어간 값이 먼저 출력:__LIFO__)   
   queue-앞에서부터 꺼낸다(가장 먼저 들어간 값이 먼저 출력:__FIFO__)     

   stack은 나중에 들어간 값이 먼저 나와야 하기 때문에 뒤에서부터 검색을 하고, queue은 먼저 들어간 값이 먼저 나와야 하기 때문에 앞에서부터 검색을 합니다. stack과 queue는 __순차적__ 으로 값을 꺼내기 위해 꺼낼 위치를 지정하는 자료구조라 __index를 사용하여 중간에 있는 값을 꺼내겠단 생각__ 으로 *stack과 queue를 사용하는 것*은 __올바르지 않습니다__.   

1. # list로 작성 - queue
   ```java 
      List<Integer> list = new LinkedList<Integer>();
         
      list.add(1); //<-- queue
      list.add(2);
      list.add(3);

      /* remove는 값을 꺼내오고 list에서 삭제 */
      System.out.println(list); //[1, 2, 3]

      System.out.println(list.remove(0)); //1
      System.out.println(list); //[2, 3]

      System.out.println(list.remove(0)); //2
      System.out.println(list); //[3]

      System.out.println(list.remove(0)); //3
      System.out.println(list); //[]

      //System.out.println(list.remove(0)); error발생
   ```
1. # list로 작성 - stack
   ```java
      List<Integer> list = new LinkedList<Integer>();

      list.add(1); 
      list.add(2);
      list.add(3); //<-- stack
      
      System.out.println(list); //[1, 2, 3]
      
      System.out.println(list.remove(list.size()-1)); //3
      System.out.println(list); //[1, 2]
      
      System.out.println(list.remove(list.size()-1)); //2
      System.out.println(list); //[1]
      
      System.out.println(list.remove(0)); //1
      System.out.println(list); //[]
      
      //System.out.println(list.remove(0)); error발생
   ```
1. # Queue
   자바에서 queue는 인터페이스로만 제공합니다. queue를 상속 받은 클래스로는AbstractQueue, ArrayBlockingQueue, ArrayDequeue, DelayQueue,LinkedBlockingDeque, LinkedList 등이 있습니다.   

   |        |Throws exception|Returns special value|
   |:------:|:--------------:|:-------------------:|
   |<B>Insert</B> |  add(e)  |       offer(e)      |
   |<B>Remove</B> | remove() |       poll()        |
   |<B>Examine</B>| element()|       peek()        |

   데이터 삽입 시 add와 offer 기능은 같지만 에러 발생시 add는 예외 처리를 하고, offer는 false를 반환합니다.   
   데이터 삭제 시 remove와 poll 기능은 같지만 에러 발생시 remove는 예외 처리를 하고, poll은 null을 반환합니다.   
   데이터 조회 시 element와 peek 기능은 같지만 에러 발생시 element는 예외 처리를 하고, peek는 null을 반환합니다.   

   ```java
      Queue<Integer> queue = new LinkedList<Integer>();
		 
		 /* offer(e)-element를 추가*/
		 System.out.println(queue.offer(1)); //true
		 System.out.println(queue.offer(2)); //true
		 System.out.println(queue.offer(3)); //true
		 System.out.println(queue.offer(1)); //true
		 System.out.println(queue); //[1, 2, 3, 1]
		 
		 /* peek()-꺼낼 element를 조회 */
		 System.out.println(queue.peek()); //1
		 
		 /* poll()-element를 꺼내오고 queue에서 삭제, 더이상 값이 없으면 null반환 */ 
		 System.out.println(queue.poll()); //1
		 System.out.println(queue.poll()); //2
		 
		 System.out.println(queue.peek()); //3,peek로 다음 나올 값을 조회
		 System.out.println(queue.poll()); //3
		 
		 System.out.println(queue.poll()); //1
		 System.out.println(queue.poll()); //queue에 값이 없으면 null반환
       System.out.println(queue.peek()); //null 반환

       queue.isEmpty(); //true, false반환
   ```
1. # stack 
   stack은 클래스로 제공되며 Vector를 상속받았습니다.

   empty() - Tests if this stack is empty.   
   peek() - Looks at the object at the top of this stack without removing it from the stack.   
   pop() - Removes the object at the top of this stack and returns that object as the value of this function.   
   push(E item) - Pushes an item onto the top of this stack.   
   
   ```java
		Stack<Integer> stack = new Stack<Integer>();
		
		/* push(e)-stack에 값을 입력 */
		stack.push(1);
		stack.push(2);
		stack.push(3);
		stack.push(1);
		System.out.println(stack); //[1, 2, 3, 1]

		/* peek()-꺼낼 element를 조회 */
		System.out.println(stack.peek()); //1
		
		/* pop()-stack에서 값을 꺼낼 때 */
		System.out.println(stack.pop()); //1
		System.out.println(stack.pop()); //3
		
		System.out.println(stack.peek()); //2, peek로 꺼낼 값 조회
		System.out.println(stack.pop()); //2
		
		System.out.println(stack.pop()); //1
		System.out.println(stack.pop()); //error, stack에 값이 없는데 pop를 하면 error발생
      System.out.println(stack.peek()); //error 발생

      stack.empty(); //true, false반환
   ```   

1. # stack과 queue 비교
   ```java
      Stack<Integer> stack = new Stack<>();

      Queue<Integer> queue = new Queue<>();
   ```   
   stack은 비었을 때 peek()나 pop()를 하면 error 발생   
   queue는 비었을 때 peek()나 poll()을 하면 null 반환   

   stack은 peek()나 pop() 사용 전에 비었는지 체크   

   stack는 empty(), isEmpty() 사용   
   queue는 isEmtpy() 사용   

1. # stack 정렬
   ```java
      Stack<Integer> s = new Stack<>();
        s.push(12);
        s.push(6);
        s.push(14);
        s.push(8);

        Collections.sort(s); //[6, 8, 12, 14] 오름차순 정렬
        s.pop(); //14

        Collections.sort(s, Collections.reverseOrder()); //[12, 8, 6] 내림차순 정렬
        s.pop(); //6
   ```   
   오름차순 정렬이든 내림차순 정렬이든 pop를 하게 되면 항상 마지막에 위치한 값이 출력됩니다.   

1. # Deque
   queue와 stack 방식을 합쳐놓은 자료구조입니다. 가장 먼저 들어온 값을 꺼내면서 가장 나중에 들어온 값도 꺼내야 할 때 사용합니다. 
   인터페이스로만 제공됩니다. Deque를 상속받은 클래스는 ArrayDeque, ConcurrentLinkedDeque, LinkedList 등이 있습니다.   
   먼저 들어간 요소 조작    
   offerfirst(e), pollFirst(), peekFirst()   
   나중에 들어간 요소 조작   
   offerList(e), pollLast(), peekList()   
   ```java
      Deque<Integer> deque = new LinkedList<Integer>();
		
		/* offerFirst-가장 앞 위치에 삽입, offerLast-가장 뒤 위치에 삽입 */
		System.out.println(deque.offerFirst(1)); //true
		System.out.println(deque.offerFirst(2)); //true
		System.out.println(deque.offerLast(3)); //true
		System.out.println(deque.offerLast(4)); //true		
		System.out.println(deque); //[2, 1, 3, 4]
		
		/* peekFirst-가장 앞 위치에 요소 검색, peekLast-가장 뒤 위치에 요소 검색 */
		System.out.println(deque.peekFirst()); //2
		System.out.println(deque.peekLast()); //4
		
		/* pollFirst-가장 앞 위치 요소 출력, pollLast-가장 뒤 위치 요소 출력 */
		System.out.println(deque.pollFirst()); //2
		System.out.println(deque.pollLast()); //4
		System.out.println(deque.pollFirst()); //1
		System.out.println(deque.pollLast()); //3

      System.out.println(deque.pollFirst()); //null, 요소가 없으면 null반환
		System.out.println(deque.pollLast()); //null, 요소가 없으면 null반환
   ```
1. # Queue,Deque,Stack 정리
   Queue - 앞에서 출력: offer(입력), poll(출력), peek(조회)   
   Stack - 뒤에서 출력: push(입력), pop(출력), peek(조회)   
   Deque - 양방향: offerFirst/offerLast, pollFirst/pollLast, peekFirst/peekLast
   Queue,Deque는 인터페이스로 제공, Stack는 클래스로 제공   
   Queue,Deque는 데이터가 없는데 poll하면 null반환, Stack는 데이터가 없는데 pop하면 error 발생   
