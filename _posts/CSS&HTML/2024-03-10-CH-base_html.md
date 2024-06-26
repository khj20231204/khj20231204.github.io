---
layout: single
title: (HTML)기본태그
categories: CSS&HTML
tag: []
---

1. # ch01.요약   
   1.웹의 이름이 뜻하는 바는?   
   <span style="color:#E8F5FF">
   웹은 사전적으로 거미줄입니다. 거미줄처럼 연결된 인터넷에서 서로 정보를 교환한다는 뜻입니다. www는 world wide web입니다. 세상의 모든 컴퓨터를 거미줄처럼 연결하여 정보를 교환한다는 뜻을 웹이라고 합니다. 정보를 제공하는 쪽을 웹서버, 요청하는 쪽을 웹클라이언트라고 합니다.   
   </span>

   2.인터넷은 무엇이며, 웹과 다른 것은?   
   <span style="color:#E8F5FF">
   인터넷과 웹은 기본적으로 다릅니다. 인터넷은 고속도로망이고, 웹은 고속도로망을 이용하는 택배 서비스로 비유할 수 있습니다. 인터넷은 IP주소를 이용하여 데이터를 전송할 수 있는 기본 통신망이고, 웹은 이 통신망 위에서 이루어지는 서비스 중의 하나입니다. 웹 이전에 이미 인터넷인란 통신망은 존재했습니다.   
   </span>

1. # ch02
   2. DOCTYPE
      ```html
         <!DOCTYPE html>
      ```   
      브라우저에게 HTML5 문서임을 알리는 지시어   
   
   2. 태그와 속성은 대소문자 구분이 없음   
      ```html
         <inPUT type="Text">
         <INput Type="text>
      ```   
      태그명과 속성 값들은 대소문자 구분이 없습니다.   
   
   2. 속성 값에서 이중 인용 부호(" ") 사용   
      ```html
         <img src=abc.jpg>
         <img src='abc.jpg'>
         <img src="abc.jpg">
      ```   
      속성 값에 부호가 없어도 되고, 단일 인용 부호도 사용되고, 이중 인용 부호도 사용이 됩니다. 모두 상관없이 동작합니다. 하지만 속성값에 빈칸이 있는 경우 이중 인용 부호를 반드시 사용해야 합니다.   
      ```html
         <img src="a b c.jpg">
      ```   
      공식적으로 이중 인용 부호를 사용할 것을 권하고 있습니다.   
   
   2. 툴팁 달기, title 속성   
      ```html
         <h1 title="툴팁이 나타난다">여기에 마우스를 올리세요</h1>
      ```   
      <h1 title="툴팁이 나타난다">여기에 마우스를 올리세요</h1>   
   
   2. 단락 나누기 p
      ```html
         <p>
         여기까지가 끝인가보오, 
         이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소 하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
         혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
         </p>
         <p>
         기나긴 그대 침묵을 이별로 받아 두겠소 
         행여 이 맘 다칠까 근심은 접어두오
         사랑한 사람이여, 더 이상 못 보아도 사실 그대 있음으로 힘겨운 날들을 견뎌왔음에 감사하오
         </p>
      ```   
      <p>
      여기까지가 끝인가보오, 
      이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소 하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
      혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
      </p>
      <p>
      기나긴 그대 침묵을 이별로 받아 두겠소 
      행여 이 맘 다칠까 근심은 접어두오
      사랑한 사람이여, 더 이상 못 보아도 사실 그대 있음으로 힘겨운 날들을 견뎌왔음에 감사하오
      </p>
   
   2. 개발자 포맷 그대로 출력   
      pre이외에 다른 태그들은 탭, `' ', <enter>`를 전부 하나의 빈칸으로 처리합니다   
      ```html
         <p>
         여기까지가 끝인가보오, 
            이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소   
               하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
                  혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
         </p>
         <pre>
         여기까지가 끝인가보오, 
            이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소   
               하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
                  혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
         </pre>
      ```   
      <p>
      여기까지가 끝인가보오, 
         이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소   
            하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
               혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
      </p>
      <pre>
      여기까지가 끝인가보오, 
         이제 나는 돌아서겠소 억지 노력으로 인연을 거슬러 괴롭히지는 않겠소   
            하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서 
               혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
      </pre>
   
   2. 블록 태그와 인라인 태그   
      블록태그 : 항상 새 라인에서 시작하고 브라우저의 왼쪽 끝에서 오른쪽 끝까지 블록 공간으로 차지합니다.   
      종류 : `<p> <h1> <div>`   
      인라인태그 : 블록에 삽입되고 블록 콘텐츠의 일부로 표현됩니다.   
      종류 : `<img> <a> <span>`
      - 많이 사용하는 블록 태그, `<div>`   
         블록을 묶는데 p태그와 div태그가 많이 사용되지만, p태그는 문단을 나누기 위해서 사용되고 div는 아무 의미 없이 문단 전체에 css를 적용하기 위해 컨테이너를 구성할 때 사용합니다.   
      - 많이 사용하는 인라인 태그 , `<span>`   
         텍스트 일부분에 특별한 모양을 주거나, 자바스크립트로 텍스트 일부분을 제어하기 위해 사용됩니다.   
      ```html
         <div style="back-gournd:skyblue">
         여기까지가 끝인가보오, 
         이제 나는 돌아서겠소 <span style="color:red">억지 노력으로 인연을 거슬러</span> 괴롭히지는 않겠소   
         <span style="color:red">하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서</span> 
         혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
         </div>
      ```   
      <div style="back-gournd:skyblue">
      여기까지가 끝인가보오, 
      이제 나는 돌아서겠소 <span style="color:red">억지 노력으로 인연을 거슬러</span> 괴롭히지는 않겠소   
      <span style="color:red">하고 싶은 말, 하려 했던 말 이대로 다 남겨 두고서</span> 
      혹시나 기대도 포기하려하오, 그대 부디 잘 지내시오
      </div>
   
   2. base   
      ```html
         <head><base href="www.mysite.com/subject/"></head>
         <a href="math.html">수학</a>
         <a href="eng.html">영어</a>
      ```   
      수학과 영어를 클릭하면  base url에 있는 주소 뒤에 현재 주소가 붙습니다.   
      www.mysite.com/subject/math.html   
      www.mysite.com/subject/eng.html   

   2. 메타 데이터   
      메타 데이터는 데이터를 설명하는 데이터입니다. `<meta>`태그는 저작자, 인토딩 방식, 문서 내용 등 다양한 메타 데이터를 나타내기 위해 사용됩니다. name과 content의 속성 쌍으로 구성되어 있습니다.   
      1. ## 작성자
      ```html
         <meta name="hyunjin" content="author">
      ```
      1. ## 검색 엔진 키워드 등록
      ```html
         <meta name="keyword" content="파이썬,자바,머신러닝">   
      ```
      name속성에 keyword를 입력하면 content에 있는 내용을 검색 엔진이 찾아 웹 사이트에 노출시킵니다.   
      1. ## 인코딩 설정
      ```html
         <meta charset="utf-8">
      ```
      해당 웹 사이트를 utf-8형식으로 인코딩 합니다.   
      1. ##  검색된 경우 추가 설명 노출
      ```html
         <meta name="description" content="추가적인 설명 기록">
      ```
      브라우저가 해당 사이트를 검색한 경우 검색된 사이트가 어떤 사이트인지 추가 설명을 표시해줍니다.   
      1. ## 모바일 지원
      ```html
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
      ```
      모바일에서도 접근할 수 있도록 반응형 웹을 사용하기 위해 viewport를 사용하여 선언   
      


   
