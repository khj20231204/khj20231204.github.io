---
layout: single
title: 리액트 첫 블로그
categories: REACT
tab: [react]
---

1. 페이지 방식 
   1. __전통적인 페이지__ <br>
   최초에 서버로부터 HTML을 전달 받고 페이지 변경이 필요할 때 다시 서버에 요청하여 HTML을 전달 받습니다.
   <u>이 과정에서 페이지를 처음부터 다시 불러오게 됩니다.</u>

   1. __SPA(single Page Application)__ <br>
   최초에 서버로부터 HTML을 전달 받고 페이지의 변경이 필요할 때 변경이 필요한 부분을 JSON으로 전달 받습니다.
   <u>이때 페이지에서 변경된 부분만 계산하여 다시 그리게 됩니다.</u>

1. React가 뭔가요? <br>
    __사용자 인터페이스를 만들기 위한 JavaScript 라이브러리__

    - ## Component
    React에서 서비스를 개발하는 데 있어 독립적인 단위로 쪼개어 구현

    - ## Virtual DOM
    가상적인 표현을 메모리에 저장하고 ReactDOM과 같은 라이브러리에 의해 실제 DOM과 동기화 개념

    - ## JSX
    Javascript에서 HTML을 사용할 수 있게 하는 기능
