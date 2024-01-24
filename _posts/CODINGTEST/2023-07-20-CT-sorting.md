---
layout: single
title: 정렬
categories: CODINGTEST
tag: [sort]
---

1. # 정렬
   정렬이란 임의의 순서대로 배열되어 있는 집합의 원소들을 일정한 순서대로 재배치하는 것을 말합니다. 정해진 규칙이란 일반적으로 크게 2가지입니다.   
   값이 점점 올라가는 방식으로 정렬 - 오름차순(ascending)   
   값이 점점 내려가는 방식으로 정렬 - 내림차순(descending)   
   정렬 알고리즘에는 수 많은 알고리즘이 존재하고 지금도 만들어지고 있습니다. 가장 빠른 알고리즘이라고 알려진 정렬 기법은 퀵 정렬이 있습니다. 하지만 퀵 정렬은 기존 원소들이 거의 정렬되어 있는 상태에서는 기존의 정렬(예로 들면 삽입 정렬)보다 뛰어난 성능을 발휘하지 못 합니다. 이렇듯 일반 해는 존재하지 않고, 상황에 따라 최적의 정렬 알고리즘이 있을 뿐입니다.    
   간단한 알고리즘으로는 선택 정렬, 삽입 정렬, 거품 정렬, 셀 정렬 등이 있고, 복잡한 알고리즘으로는 퀵 정렬, 기수 정렬, 힙 정렬, 병합 정렬 등이 있습니다.   
   간단한 알고리즘은 구현이 쉽고 안정되어 있지만 속도가 느리고, 복잡한 알고리즘은 구현은 어렵지만 속도면에서 뛰어납니다. 정렬 알고리즘을 삽입, 교환, 병합, 선택으로 구분하면 다음과 같습니다.   

   |   삽입     |    교환    |     병합    |     선택    |      세기     |
   |:----------:|:----------:|:----------:|:----------:|:----------:|
   |삽입 정렬<br>쉘 정렬|거품 정렬<br>퀵 정렬<br>기수 교환 정렬|병합 정렬|선택 정렬<br>힙 정렬|분포수 세기<br>직접 기수 정렬|   
      
1. # 선택 정렬(Selection sort)
   가장 간단한 알고리즘이며 일상 생활에서 가장 많이 알고리즘 일 수 있습니다. 최소값을 찾아서 가장 앞쪽에 두는 방식입니다(오름차순 일때). 탐색은 인덱스로 하게 됩니다. 즉, __인덱스로 탐색 후 최소값을 선택하여 가장 앞쪽으로 이동__ 시키기 때문에 선택 정렬이라 합니다.
   선택 정렬의 비교 횟수는 최소값을 찾기 위해서 반복문을 두 번 사용하기 때문에 N²/2정도로 많지만, 교환 횟수는 많아야 전체가 한번 바뀌는 경우인 N번 입니다. 교환 횟수 N번은 정렬 알고리즘에서 상당히 작은 횟수에 속합니다. 이것이 선택 정렬의 장점입니다.   
   시간 복잡도는 반복문을 2번 실행하기 때문에 O(N²)이 됩니다.   
   <br>
   3&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4 를 오름차순으로 정렬해보겠습니다.   
   <br>
   해당 범위는 index 0부터 끝가지가 됩니다. 이 범위에서 최소값을 찾습니다.   
   __3__&nbsp;&nbsp;&nbsp;__1__&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;__4__   
   최소값은 1이 됩니다. 1을 가장 왼쪽으로 이동시킵니다.   
   __1__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   1의 정렬은 끝났습니다.   
   <br>
   해당 범위는 index 1부터 끝까지가 됩니다. 이 범위에서 최소값을 찾습니다.   
   1&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;__4__   
   최소값은 2가 됩니다. 2를 현재 범위에서 가장 왼쪽인 index 1로 이동시킵니다.   
   1&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;4   
   2의 정렬은 끝났습니다.   
   <br>
   해당 범위는 index 2부터 끝까지가 됩니다. 이 범위에서 최소값을 찾습니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__4__   
   최소값은 3이 됩니다. 3의 index가 현재 범위에서 가장 왼쪽인 index 2이므로 자리 이동은 없습니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;4   
   3의 정렬은 끝났습니다.   
   <br>
   해당 범위는 index 3부터 끝까지가 됩니다. 이 범위에서 최소값을 찾습니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__4__   
   최소값은 4가 됩니다. 4를 현재 범위에서 가장 왼쪽인 index 3으로 이동시킵니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;5   
   4의 정렬은 끝났습니다.   
   <br>
   마지막인 5는 해당 범위의 끝이 됩니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;__5__   
   5의 정렬은 끝났습니다.   
   <br>
   최소값을 찾기 위해 n번을 돌고 다시 정렬을 하기 위해 n번을 돌기 때문에 for문을 2번 돌게 됩니다. 시간복잡도는 역시 __n(O²)__ 이 됩니다.

1. # 버블 정렬(bubble sort)
   가장 단순하고 시간이 오래 걸리지만 가장 확실한 방법입니다. 성능은 가장 떨어지지만 가장 확실한 방법입니다.   
   버블정렬은 __기준이 변경__ 됩니다. 비교하는 과정에서 기준 값보다 비교값이 더 작으면 기준과 비교값의 자리를 바꾸고 기준을 비교값으로 이동시킵니다. 기준 값이 거품이 생기듯이 여기 저기서 계속 생기기 때문에 버블정렬이라 합니다.   
   최악의 경우는 역순 배열의 경우입니다. 이때 비교 횟수와 교환 횟수는 n(n-1)/2가 됩니다. 첫항이 0이고 등차가 1인 1부터 n항까지 모든 항을 더하는 등차수열의 합이므로 n(n-1)/2가 나오게 됩니다.   
   이중 루프를 돌기 때문에 시간 복잡도는 O(n²)이 됩니다.   
   <br>
   3&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;오름차순으로 버블정렬을 하겠습니다.   
   <br>
   __3__&nbsp;&nbsp;&nbsp;__1__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;3을 기준으로 1과 비교합니다. 1이 더 작기 때문에 자리바꿈을 합니다.   
   __1__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;자리바꿈한 1을 기준으로 5와 비교를 합니다.   
   __1__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;자리바꿈한 1과 2를 비교합니다.   
   __1__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;자리바꿈한 1과 4를 비교합니다. 1은 모든 비교가 끝났기 때문에 옆자리 3을 기준으로 비교를합니다.   
   <br>
   1&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;3을 기준으로 5와 비교를 합니다.   
   1&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;3을 기준으로 2와 비교를 합니다. 2가 더 작기 때문에 3과 2의 자리를 바꿉니다.   
   1&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;자리바꿈한 2를 기준으로 계속 비교를 합니다. 4가 더 크기 때문에 자리바꿈하지 않습니다. 2는 모든 비교가 끝났습니다.   
   <br>
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;5를 기준으로 3과 비교를 합니다. 3이 더 작기 때문에 자리바꿈을 합니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;3을 기준으로 4와 비교를 합니다. 3은 모든 비교가 끝났습니다.   
   <br>
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;5를 기준으로 4와 비교를 합니다. 4가 더 작기 때문에 자리바꿈을 합니다.   
   <br>
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;:&nbsp;&nbsp;&nbsp;끝자리 5를 기준으로 정렬을 합니다.   마지막 숫자이므로 정렬이 완료 되었습니다.   
   <br>
   for문을 2번 실행해야 하기 때문에 시간복잡도는 __O(N²)__ 이 됩니다.   

1. # 삽입 정렬(Insertion sort)
   선택 정렬이 많은 비교와 적은 교환으로 이루어진다면, 삽입 정렬은 적은 비교와 많은 교환으로 이루어집니다. 삽입 정렬은 처음 선택한 __기준이 고정__ 되어 있습니다. 처음 선택한 기준이 비교값보다 작으면(오름차순) 왼쪽으로 이동을 하기 때문에 "기준 값이 변경되지 않고 이동하여 삽입된다"라고 할 수 있습니다. 삽입 정렬은 이미 정렬된 배열일 경우 속도가 아주 빠릅니다. 이미 정렬된 경우에는 삽입 정렬의 실행 시간은 N에 비례합니다. 역순의 경우가 최악이 되며 비교와 교환 횟수는 n(n-1)/2가 됩니다. 선택 정렬보다 속도가 떨어집니다. 삽입 정렬의 시간 복잡도는 O(N²)이 됩니다.
   최초 인덱스를 0이 아닌 1로 잡고 오른쪽 값들과 비교 후 값을 하나씩 옮겨가는 방식입니다.   
   <br>
   3&nbsp;&nbsp;&nbsp;1&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;를 오름차순으로 정렬해보겠습니다.   
   <br>
   최초 인덱스를 0이 아닌 1로 잡고 왼쪽 값과 비교를 합니다.   
   3&nbsp;&nbsp;&nbsp;__1__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   1을 3과 비교합니다. 1이 더 작기 때문에 왼쪽으로 이동합니다.   
   __3__&nbsp;&nbsp;&nbsp;__1__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   1의 정렬은 끝이 났습니다.    
   1&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   <br>
   인덱스 값이 2인 5를 기준으로 비교를 합니다.   
   1&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   5와 3을 비교합니다. 5가 더 크기 때문에 자리 이동은 없습니다.   
   1&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   5의 정렬은 끝이 났습니다.   
   1&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;4   
   <br>
   인덱스 값이 3인 2를 기준으로 비교를 합니다.   
   1&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;4   
   2와 5를 비교합니다. 2가 더 작기 때문에 왼쪽으로 이동합니다.   
   1&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__5__&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;4   
   2와 3을 비교합니다. 2가 더 작기 때문에 왼쪽으로 이동합니다.   
   1&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;4   
   2와 1을 비교합니다. 2가 더 크기 때문에 자리 이동은 없습니다.   
   __1__&nbsp;&nbsp;&nbsp;__2__&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;4   
   2의 정렬은 끝이 났습니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;4   
   <br>
   인덱스 값이 4인 4를 기준으로 비교를 합니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;5&nbsp;&nbsp;&nbsp;__4__   
   4와 5를 비교합니다. 4가 더 작기 때문에 왼쪽으로 이동합니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;__5__   
   4와 3을 비교합니다. 4가 더 크기 때문에 자리 이동은 없습니다.   
   1&nbsp;&nbsp;&nbsp;2&nbsp;&nbsp;&nbsp;__3__&nbsp;&nbsp;&nbsp;__4__&nbsp;&nbsp;&nbsp;5   
   모든 정렬이 끝났습니다.   
   <br>
   버블정렬과 방식이 비슷합니다. 시간복잡도는 for문을 2번 돌아야하기 때문에 __O(n²)__ 이 됩니다.   

1. # 퀴 정렬(Quick sort)
   퀵 정렬은 아주 빠른 속도를 낼 뿐만 아니라, 원리도 간단하기 때문에 많은 분야에서 응용되는 정렬 방법입니다. 퀵 정렬의 핵심은 __분할__ 입니다. 축(Pivot)값을 중심으로 축 값보다 작으면 왼쪽, 크면 오른쪽으로 정렬시킵니다(오름차순 기준). 재귀적 용법을 사용하고, 멀리 떨어져 있는 요소끼리 교환을 하기 때문에 빠른 정렬 상태가 됩니다. pivot은 값을 임의로 선택 후 이 값을 기준으로 나뉘게 됩니다.   
   가장 이상적인 경우는 양쪽이 크기 순으로 분할되어 있는 경우로 이때 재귀의 깊이는 log₂N이 됩니다. 퀴 정렬의 일반적인 경우는 O(NlogN)입니다.   
   
1. # 병합 정렬(Merge sort)
   병합 정렬은 두 파일을 병합하는 과정을 일반화 한 것입니다. 병합 정렬은 자료 배열에 접근하는 것이 순차적이어서 연결 리스트와 같은 순차적 접근만이 가능한 자료 구조에 유일한 정렬 방법입니다.    
   배열된 원소들을 왼쪽과 오른쪽으로 재귀적으로 나눈 후 1개씩 전부 쪼개졌을 때 다시 비교를 해서 정렬하면서 병합을 하는 방식입니다.   

1. # 시간 복잡도

   |   Name  |  Best | Average| Worst |
   |:-------:|:-----:|:------:|:-----:|
   | Bubble  |   N   |   N²   |   N²  |
   |Insertion|   N   |   N²   |   N²  |
   |Selection|   N²  |   N²   |   N²  |
   |  Quick  | NlogN | NlogN |    N²  |
   |  Merge  | NlogN | NlogN | NlogN |



