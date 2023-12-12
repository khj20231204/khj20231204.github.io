---
layout: single
title: 정렬
categories: CODINGTEST
tag: [sort]
---

1. # 정렬
   값이 점점 올라가는 방식으로 정렬 - 오름차순 정렬(ascending)   
   값이 점점 내려가는 방식으로 정렬 - 내림차순 정룔(descending)   
1. # 버블정렬(bubble sort)
   가장 단순하고 시간이 오래 걸리지만 가장 확실한 방법입니다.    
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
   for문을 2번 실행해야 하기 때문에 시간복잡도는 __n(O²)__ 이 됩니다.   
1. # 삽입정렬(Insertion sort)
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
   버블정렬과 방식이 비슷합니다. 시간복잡도는 for문을 2번 돌아야하기 때문에 __n(O²)__ 이 됩니다.   
1. # 선택정렬(Selection sort)
   최소값을 찾아서 가장 왼쪽에 두는 방식입니다. 해당 범위에서 최소값을 찾은 후 가장 왼쪽으로 이동시킵니다.   
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
1. # 퀴정렬(Quick sort)
   작은 것들은 작은 것들끼리, 큰 것들은 큰 것들끼리 구분 지은 후 그 안에서 정렬을 합니다.
   pivot이란 값을 임의로 선택 후 이 값을 기준으로 나뉘게 됩니다.


