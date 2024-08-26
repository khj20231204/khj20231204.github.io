---
layout: single
title: 내부 클래스
categories: JAVA
tag: 
---

1. # 

1. # static함수에서 내부 클래스 사용
   static함수에서 내부 클래스를 사용하면 error가 발생합니다.   

   ```java
      public class SortingNode {

         class Node{	                 //내부 클래스
            String name;
            
            public Node(String n) {
               name = n;
            }
         }
         
         public static void main(String[] args) {  //static 함수에서 내부 클래스 사용

            List<Node> nodes = new ArrayList<>();

            nodes.add(new Node("A")); //new Node("A")에서 error발생
         }
         
         public void a() {          //일반 함수
            List<Node> nodes = new ArrayList<>();

            nodes.add(new Node("A"));  //error발생하지 않음
         }
      }
   ```   
   main인 static함수에 new Node()를 사용하면 error가 발생하고 static이 아닌 일반 함수에서 new Node()를 사용하면 error가 발생하지 않습니다.   
   그 이유는 멤버 내부 클래스는 외부 클래스의 인스턴스가 필요하며, 외부 클래스의 인스턴스를 통해 생성되기 때문입니다. static

   