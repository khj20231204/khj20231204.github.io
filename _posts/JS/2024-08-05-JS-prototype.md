---
layout: single
title: prototype
categories: JS
tag: []
---
 
1. # 프로토타입
   생성자함수를 이용해 new연산자로 객체의 인스턴스를 생성하면 이 인스턴스 내부에 constructor의 'prototype'이라고 하는 프로퍼티의 내용이 [[Prototype]]라고 하는 프로퍼티로 참조를 전달하게 됩니다.   

   *constructor   
   객체를 생성하는데 가장 먼저 호출되는 메소드   

   Constructor(prototype)    
   &nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|   
   &nbsp;&nbsp;&nbsp;&nbsp;|  new&nbsp;&nbsp;&nbsp; |   
   &nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|   
   &nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;|   
   instance [[prototype]]   

   Constructor.prototype와 instance[[prototype]]이 같은 객체를 가리킵니다. 하지만 [[prototype]]는 접근가능한 것이 아니라 정보를 보여주기만 할 뿐으로 실제 동작상으로는 instance와 동일시가 됩니다.   

   왼쪽 - 생성자, 오른쪽 - 생성자의 prototype   
   아래쪽 - 인스턴스   

   