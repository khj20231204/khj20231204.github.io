---
layout: single
title: 선형탐색
categories: CODINGTEST
tag: [LinkedList]
---

1. # 이진탐색
    중간값을 찾는값과 비교, 찾는값이 중간값 보다 더 작으면 중간값 보다 작은 영역에서 다시 중간값을 잡고 찾는값과 비교, 찾는값이 중간값 보다 더 크면 중간값보다 더 큰 영역에서 다시 중간값을 잡고 찾는값과 비교, 이 작업을 반복
    ```java
       public int linearSearchBasic(int[] nums, int s){
            // start, end, mid는 idx값
            int start = 0;

            /*
            length-1이든 length든 상관없다. 제일 처음 mid 값만 정할 때 사용
            개수가 짝수인 경우 mid값 - length-1 : mid-1, length: mid+1
            개수가 홀수인 경우 mid값 - length-1과 length 모두 mid
             */
            int end = nums.length;

            while(start < end){
                int mid = (end-start)/2 + start;
                System.out.println("mid:"+mid);
                int v = nums[mid];
                if(v == s) return mid;

                if(s < v) end = mid;
                else start = mid+1;
            }
            return -1;
        }
    ```
1. # comparable인터페이스 상속
    java에서 binarySearch는 Collections클래스에 정의 되어있습니다. Collections클래스를 사용하기 위해선 Comparable<T> 인터페이스를 상속받아서 compareTo 메서드를 재정의 해줘야 Collections.sort(), Collections.binarySearch() 메서드 등을 사용할 수 있습니다.   
    ●MyClass에서 Comparable인터페이스 상속받아서 compareTo재정의 하기●   
    ```java
        class MyData implements Comparable<MyData>{ //<-- Comparable<T> 상속받기, 재너릭타입에는 정렬할 클래스 타입을 넣습니다
            int v;

            public MyData(int v) {
                this.v = v;
            }

            @Override
            public String toString() {
                return "" + v;
            }
            
            @Override
            public int compareTo(MyData o) { //<-- Comparable인터페이스의 추상 메서드
                /*
                1 == 1 : 1 - 1 == 0 (빼서 0이면 같다)
                a ? b : (a과 b의 대소관계비교)
                        : 0 (0이면 a와 b가 같다)
                        : 양수 (양수이면 a가 크다)
                        : 음수 (음수이면 b가 크다)
                */
                return this.v - o.v; //오름차순 정렬, o.v-this.v:내림차순 정렬
            }
        }
    ```   
    ●정수형을 요소로 갖는 List에 Comparable상속 다른 예시●   
    ```java
        public class MyInteger implements Comparable<Integer> {

            private int value;
            public MyInteger(int value) {
                this.value = value;
            }
            
            public int getValue() {
                return value;
            }
            
            @Override
            public int compareTo(Integer other) {
                return Integer.compare(this.value, other);
            }
        }
    ```
1. # java의 binarySearch이용하기
    ```java
        List<MyData> md2 = new LinkedList<>();
        Random r = new Random();
        for(int i=1 ; i<=10 ; i++) md2.add(new MyData(r.nextInt(1,10)));
        Collections.sort(md2); 
        int idx3 = Collections.binarySearch(md2, new MyData(5)); //리턴값은 idx값
    ```
    list를 정렬하기 위해서 Collections.sort()를 사용해야합니다. MyData에서 Comparable를 상속받아 compareTo를 재정의 했기 때문에 sort()와 binarySearch()를 사용할 수 있습니다.
