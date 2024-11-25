---
layout: single
title: thymeleaf
categories: SPRINGBOOT
tag: []
author_profile: false
---

1. # 작동방식
   ```html
      <Tag th:text="${변수}">여기 출력값은 무시</Tag>
   ```
   태그 안에 th속성을 이용하여 값을 출력합니다. `<Tag></Tag>`로 둘러싸인 값은 어떤 값이든 무시가 됩니다. 태그 안에 다른 문자열이 함께 존재하더라도 th:text 속성의 값만 출력됩니다. 이는 Thymeleaf가 서버 사이드 템플릿 엔진으로, 서버에서 데이터를 동적으로 바인딩하여 최종 HTML을 생성하기 때문입니다. th:text 속성이 있는 태그 안에 다른 문자열이 존재하더라도 무시되고, th:text 속성의 값만 출력됩니다.   

1. # 저장 위치
   확장자는 html파일로 templates위치에 저장되야합니다.   

1. # 단순 글자 출력
   -Controller.java-   
   ```java
      @Controller
      public class SampleController {

         @RequestMapping("/textprint")
         public String textprint(Model model) {
            
            model.addAttribute("greeting", "Hello");
            model.addAttribute("greeting_hangul", "안녕 하세욬");
            
            return "textprint"; //resources/templates/sample1.html로 가게 된다. resources/templates/는 필수 경로
         }
      }
   ```

   -textprint.html-   
   ```html
      <body>
         <h1>Thymeleaf Test page</h1>
         1.<th:${greeting}> <!--태그가 없기 때문에 아무 값도 출력 되지 않음 -->
         <br>
         2.<th:text=${greeting}> <!--태그가 없기 때문에 아무 값도 출력 되지 않음 -->
         <br>
         3.<t th:text=${greeting}>여기 값들은 다 무시</t> <!-- t는 의미없는 범위 설정 태그 -->
         <br>
         4.<u th:text=${greeting}>여기 값들은 다 무시</u> <!-- u는 밑줄 태그 -->
         <br>
         5.<div th:text=${greeting_hangul}>여기 값들은 다 무시</div>
      </body>

      출력 값 :
      Thymeleaf Test page
      1.
      2.
      3.Hello
      4.Hello
      5.
      안녕 하세욬
   ```

1. # dto객체 가져오기

   -Controller.java-   
   ```java
      @Controller
      public class SampleController {

         @RequestMapping("/classprint")
         public String classprint(Model model) {
            Member member = new Member(100, "myid", "1223", "길동자", new Timestamp(System.currentTimeMillis()));
            model.addAttribute("member",member);
            
            return "classprint"; //resources/templates/sample1.html로 가게 된다. resources/templates/는 필수 경로
         }
      }
   ```

   -classprint.html-   
   ```html
      <body>
         <h1>member html</h1>
         <!-- th:text : DTO 객체 출력 -->
         <h3 th:text="${member}"></h3>
         
         <!-- th:text : 문자열(HTML태그) 출력 -->
         <div th:text="${'<h3>'+member.no+'</h3>'}"></div>
         <!-- text는 문자 그대로 전부 출력 : <h3>100</h3> -->
         
         <!-- th:utext : 태그가 적용된 데이터 출력 -->
         <div th:utext="${'<h3>'+member.no+'</h3>'}"></div>
         <div th:utext="${'<h3>'+member.id+'</h3>'}"></div> 
         <div th:utext="${'<h3>'+member.pw+'</h3>'}"></div> 
         <div th:utext="${'<h3>'+member.name+'</h3>'}"></div> 
         <div th:utext="${'<h3>'+member.regdate+'</h3>'}"></div>
      </body>

      출력 값 : 
      member html
      Member(no=100, id=myid, pw=1223, name=길동자, regdate=2024-10-21 16:46:09.866)
      <h3>100</h3>
      100
      myid
      1223
      길동자
      2024-10-21 16:46:09.866
   ```

1. # 리스트 가져오기
   
   반복문을 사용하기 위해서 each를 사용합니다.   
   ```
      th:each="변수:${Collection}"
   ```

   table에 each가 있으면 table이 반복되고 , tr에 each가 있으면 tr이 반복됩니다.   
   each가 있는 위치가 반복문의 scope가 됩니다.   

   -Controller.java-   
   ```java
      @RequestMapping("/getlist")
         public String getlist(Model model) {
            
            List<Member> list = new ArrayList<>();
            
            for(int i= 0 ; i<10 ; i++) {
               Member m = new Member(i, "myid_u"+ i%3,"1234", "myname"+i%9, new Timestamp(System.currentTimeMillis()));
               list.add(m);
            }
            
            model.addAttribute("list", list);
            
            return "getlist";
         }
   ```

   -getlist.html-   
   ```html
      <table border=1 align=center>
         <tr>
            <th>no</th>
            <th>아이디</th>
            <th>비밀번호</th>
            <th>이름</th>
            <th>가입날짜</th>
         </tr>
         <tr th:each="member:${list}">
            <td th:text="${member.no}"></td>
            <td th:text="${member.id}"></td>
            <td th:text="${member.pw}"></td>
            <td th:text="${member.name}"></td>
            <td th:text="${#dates.format(member.regdate,'yyyy-MM-dd HH:mm:ss')}"></td>
         </tr>
         </table>

      출력 값 :
      no	아이디	비밀번호	이름	가입날짜
      0	myid_u0	1234	myname0	2024-10-21 16:43:03.971
      1	myid_u1	1234	myname1	2024-10-21 16:43:03.971
      2	myid_u2	1234	myname2	2024-10-21 16:43:03.971
      3	myid_u0	1234	myname3	2024-10-21 16:43:03.971
      4	myid_u1	1234	myname4	2024-10-21 16:43:03.971
      5	myid_u2	1234	myname5	2024-10-21 16:43:03.971
      6	myid_u0	1234	myname6	2024-10-21 16:43:03.971
      7	myid_u1	1234	myname7	2024-10-21 16:43:03.971
      8	myid_u2	1234	myname8	2024-10-21 16:43:03.971
      9	myid_u0	1234	myname0	2024-10-21 16:43:03.971
   ```

1. # 변수명 사용

   ```
      th:with="변수명='값'"
   ```
   th속성이 사용된 해당 태그의 범위까지가 변수의 유효 스코프가 됩니다.   

   ```html
      <table border="1" align="center" th:with="target='myid_u2'">
      <!--변수 with는 table태그 안에서 유효합니다. 변수를 포함하는 태그 안이 변수의 유효 스코프가 됩니다. -->
         <tr>
            <th>no</th>
            <th>아이디</th>
            <th>비밀번호</th>
            <th>이름</th>
            <th>가입날짜</th>
         </tr>
         <tr th:each="member:${list}">
            <td th:text="${member.no}"></td>
            <td th:text="${member.id == target ? 'secret' : member.id}"></td>
            <td th:text="${member.pw}"></td>
            <td th:text="${member.name}"></td>
            <td th:text="${#dates.format(member.regdate,'yyyy-MM-dd HH:mm:ss')}"></td>
         </tr>
      </table> 

      출력 값 : 
      no	아이디	비밀번호	이름	가입날짜
      0	myid_u0	1234	myname0	2024-10-21 17:16:15
      1	myid_u1	1234	myname1	2024-10-21 17:16:15
      2	secret	1234	myname2	2024-10-21 17:16:15
      3	myid_u0	1234	myname3	2024-10-21 17:16:15
      4	myid_u1	1234	myname4	2024-10-21 17:16:15
      5	secret	1234	myname5	2024-10-21 17:16:15
      6	myid_u0	1234	myname6	2024-10-21 17:16:15
      7	myid_u1	1234	myname7	2024-10-21 17:16:15
      8	secret	1234	myname8	2024-10-21 17:16:15
      9	myid_u0	1234	myname0	2024-10-21 17:16:15
   ```

1. # if 조건문 사용
   





     
