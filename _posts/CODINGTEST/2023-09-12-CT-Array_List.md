---
layout: single
title: array와 list
categories: CODINGTEST
tag: [array, list]
---


1. # Array 와 List 비교
   배열은 삽입/삭제 시 해당 index까지 값들의 이동을 전부 해주어야 하지만, list는 해당 노드의 앞뒤 노드와 연결만 해주면 되기 때문에 list가 유리합니다. 하지만 검색 시 index값을 알면 배열은 해당 index로 바로 접근이 가능하지만 list는 해당 노드를 찾기 위해 가장 첫 노드부터 해당 노드까지 검색을 해야하기 때문에 배열이 유리합니다. 따라서 삽입/삭제가 많은 상황에서는 list를 사용하고, 삽입/삭제 보다 조회가 많은 경우는 배열을 사용하는 것이 효율적입니다.