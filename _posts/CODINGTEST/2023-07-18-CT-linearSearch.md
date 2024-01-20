---
layout: single
title: 선형탐색
categories: CODINGTEST
tag: [LinkedList]
---

1. # 순차탐색(Sequential Search)
    선형 탐색이라고도 합니다. 찾고자 하는 검색키를 처음부터 순차적으로 끝까지 비교하며 검색하는 방법입니다. 가장 단순하고 어떠한 상황에서도 사용될 수 있는 융통성이 있지만 평균적으로 N/2번의 검색을 해야하기 때문에 효율성이 낮습니다. 검색해야 하는 전체 N이 작으면 검색 시간도 단축이 되지만 일반적인 시간 복잡도는 O(Π)이 됩니다. 비교횟수가 O(logΠ)정도인 다른 검색 방법과 큰 차이가 생깁니다.   

    searchArray배열에서 일치하는 key를 찾는 예제입니다.    
    ```java
        int search(int[] searchArray, int key){
            for(int i : SearchArray){
                if(key == i) return i;
            }
        }
    ```   
    처음 요소부터 반복문을 수행하면서 해당 요소를 찾을 때까지 반복하게 됩니다.   

1. # 완전탐색(Exhaustive Search)   
    brute-force알고리즘이라고도 합니다. 빠짐없이 모든 경우를 원하는 결과를 얻을 때까지 대입하는 알고리즘입니다. 올바른 해결책을 얻을 때 까지 체계적으로 조사를 하게 됩니다. 대입을 처음부터 순차적으로 실행하게 되면 순차탐색과 일치합니다. 완전탐색은 for문을 이용할 수도 있고, 재귀, 순열, 조합을 이용해서 해결할 수 있습니다.   

    searchArray배열에서 가장 큰 값의 key를 찾는 예제입니다.   
    ```java
        public class exhaustiveSearch{
            public static int findMax(int[] searchArray) {
                int max = searchArray[0];
                for (int i = 1; i < searchArray.length; i++) {
                    if (searchArray[i] > max) {
                        max = searchArray[i];
                    }
                }
                return max;
            }

            public static void main(String[] args) {
                int[] arr = {3, 1, 5, 2, 4};
                int max = exhaustiveSearch(arr);
                System.out.println(max);  // Output: 5
            }
        }
    ```
    for문 같은 반복문을 사용하게 되면 첫 번째 요소의 index를 대입해야 하기 때문에 순차탐색과 일치할 수밖에 없습니다. 

    순열(permutation)과 조합(combination)은 원소들의 집합을 특정 순서로 배열하는 방법입니다. 순열은 중복을 허락해서(순서가 있게) n개 중에서 r개를 꺼낼 때  n!/(n-r)!의 방법을 제공합니다. 조합은 순열에서 중복을 제거한 n!/(n-r)!r! 로 r!을 나눈 경우의 수를 제공합니다. 둘 다 특정 순서로 요소들을 뽑는데 사용할 수 있습니다. 특정 순서로 요소들을 뽑은 후 완전탐색 기법으로 모든 경우의 수를 대입하게 됩니다.   

    각각 1,2,3번호를 가진 3명이 줄을 서는데 3번이 제일 앞에 서는 경우를 구하란 예제를 순열을 통해 나타낸 예제입니다.
    ```python
        from itertools import permutations

        def brute_force_permutation(elements):
            permutations_list = list(permutations(elements))
            # Iterate over all permutations and check for desired conditions
            for permutation in permutations_list:
                if check_condition(permutation):
                    # Perform desired action with the valid permutation
                    print(permutation)

        def check_condition(permutation):
            # Implement your condition checking logic here
            # Return True if condition is satisfied, False otherwise
            # Example: Check if the first value of the elements is No.3
            return checkFirst(permutation)  == 3

        # Example usage
        elements = [1, 2, 3]
        brute_force_permutation(elements)
    ```   
    brute_force_permutation함수로 elements란 배열을 넘겨 줍니다. brute_force_permutation함수에선 가능한 모든 permutations_list를 생성 후 각각의 조건을 check_condition함수로 넘겨 3번이 제일 앞이면 true를 리턴하게 됩니다. 이때 permutation의 모든 가능한 경우를 뽑아서 원하는 값을 만족할 때까지 대입하게 되는데 완전탐색기법을 이용하게 됩니다.   

    python은 permutations와 combinations을 c++에서는 permutations를 라이브러리로 제공하지만 java는 직접 구현을 해야 합니다.   
    ```java
        public static void permute(int[] arr, int n) {
            if (n == 1) {
                for (int num : arr) {
                    System.out.print(num + " ");
                }
                System.out.println();
            } else {
                for (int i = 0; i < n; i++) {
                    int temp = arr[i];
                    arr[i] = arr[n - 1];
                    arr[n - 1] = temp;

                    permute(arr, n - 1);

                    temp = arr[i];
                    arr[i] = arr[n - 1];
                    arr[n - 1] = temp;
                }
            }
        }

        public static void main(String[] args) {
            int[] arr = {1, 2, 3};
            permute(arr, arr.length);
        }    
    ```    
    재귀적 호출을 이용해서 permutation을 구현합니다.   

    __*자바에선 Collections의 indexOf, contains, remove등의 메소드에서 이미 완전탐색이 구현되어 있습니다.__   
    그렇기 때문에 해당 메소드들을 옳바르게 사용하는 것이 중요합니다.   

1. # 이진 탐색(Binaklry Search)
    이분 검색이라고도 합니다. 이 검색법은 자료들이 크기순으로 정렬되어 있는 상태여야됩니다. 자료의 중간값을 먼저 키 값과 검사하게 됩니다. 해당 값이 아니면 중간 값보다 작으면 왼쪽으로 탐색, 크면 오른쪽으로 탐색을 합니다. 이 작업을 원하는 키 값이 나올 때까지 반복하게 됩니다. 가장 먼저 중간값을 설정하므로 원래 크기가 원래 크기의 반으로 줄어듭니다. n번 시행 후 크기는 N/2ⁿ 이 남게 됩니다. 순차 탐색은 한번의 탐색으로 N-1번 크기가 감소하며 n번 시행 후 크기는 N-n번이 남게 되는 순차 탐색과 대조적입니다. 이진 탐색의 시간 복잡도는 logΠ이 됩니다.   
    
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

1. # JAVA에서 이진 탐색 이용하기
    java에선 이진 탐색을 제공합니다. java.util 의 Collections클래스에 binarySearch메소드가 정의되어 있습니다.   

    binarySearch 정의
    ```java
        public static <T> int binarySearch(List<? extends Comparable<? super T>> list,T key)
        public static <T> int binarySearch(List<? extends T> list,T key,Comparator<? super T> c)
    ```   
    List<? extends Comparable<? super T>> list는 Comparable인터페이스를 상속받아야합니다. Comparable인터페이스는 CompareTo 메소드를 재정의해야 합니다.   

    1)comparable인터페이스 상속
    java에서 binarySearch는 Collections클래스에 정의 되어있습니다. Collections클래스를 사용하기 위해선 Comparable<T> 인터페이스를 상속받아서 compareTo 메소드를 재정의 해줘야 Collections.sort(), Collections.binarySearch() 메소드 등을 사용할 수 있습니다.   

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
            public int compareTo(MyData o) { //<-- Comparable인터페이스의 추상 메소드
                /*
                1 == 1 :Collections.sort(md2);  1 - 1 == 0 (빼서 0이면 같다)
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
    2)binarySearch로 탐색
    ```java
        List<MyData> md2 = new LinkedList<>();
        Random r = new Random();
        for(int i=1 ; i<=10 ; i++) md2.add(new MyData(r.nextInt(1,10)));
        Collections.sort(md2); 
        int idx3 = Collections.binarySearch(md2, new MyData(5)); //리턴값은 idx값
    ```
    list를 정렬하기 위해서 Collections.sort()를 사용해야합니다. MyData에서 Comparable를 상속받아 compareTo를 재정의 했기 때문에 sort()와 binarySearch()를 사용할 수 있습니다.
