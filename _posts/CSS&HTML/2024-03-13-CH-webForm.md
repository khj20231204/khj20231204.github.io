---
layout: single
title: (HTML)웹 폼
categories: CSS&HTML
tag: []
---

1. # 웹 폼과 폼 요소
   웹 페이지를 통해 사용자의 입력을 받는 페이지를 웹 폼 또는 폼이라 합니다. 폼 안에는 input, textarea, select 등 다양한 태그들을 제공하며 이를 폼 요소라고 합니다.   

1. # form 태그
   1. name 속성   
      폼 이름 지정. 서버 쪽에서 받을 변수명이 됩니다.   
   
   1. action 속성   
      폼 데이터를 처리할 웹 서버 응용프로그램 지정. submit버튼을 클릭하면 action 속성에 지정된 웹 서버 응용프로그램으로 폼 데이터를 전송   
   
   1. method 속성   
      폼 데이터를 웹 서버로 전송하는 형식을 지정합니다. 대표적으로 GET과 POST 방식이 있습니다.   

      `<form action="웹 서버 응용프로그램 주소"
            enctype="데이터의 인코딩 타입"
            method="GET/POST"
            name="폼 이름"
            target="윈도우 이름"
            >
      ...
      </form>`

      ```html
      <form name="firstForm" action="www.naver.com/sore/" method="get">
         <input type="text" name="firstData"> 
         <input type="text" name="secondData">
         <input type="submit" value="전송">
      </form>   
      ```
      <form name="firstForm" action="www.naver.com/sore/" method="get">
         <input type="text" name="firstData"> 
         <input type="text" name="secondData">
         <input type="submit" value="전송">
      </form>   

      전송 버튼을 누르면 text의 name이 변수명이 되고 텍스트 박스 안에 값이 데이터가 됩니다.   
      .../www.naver.com/sore/?firstData=one&secondData=two   
      와 같이 firstData란 이름으로 one이란 값이 넘어가고 secondData란 이름으로 two란 값이 전송됩니다.   

      *`<form>`태그 없이 사용하는 경우도 있는데 이런 경우는 웹 서버로 데이터를 전송하지 않고 자바스크립트 코드에서 사용자의 입력을 받는 것을 목적으로 사용할 때 입니다.   

1. # input태그의 속성들
   1)name 속성   
   input 태그가 서버로 전송될 때 해당 태그를 각각 구분할 수 있는 기준이됩니다.   
   name 속성은 `<select>` 태그, `<textarea>` 태그 등 모든 입력 태그에 사용   
   ```html
      <input name="data">
   ```   

   2)placeholder 속성   
   input 박스 안에 미리 입력되어 있는 예제를 설정   
   ```html
      <input placeholder="example@example.com">
   ```   
   <input placeholder="example@example.com"> 
      
   3)value   
   input 태그에 기본값을 지정할 때 사용. 다양한 type에 사용      
   ```html
      <input value="기본값">
      <input type="date" value="2024-03-07">
   ```
   <input value="기본값">   
   <input type="date" value="2024-03-07">

   4)disabled   
   요소들을 비활성화하기위한 명령어   
   input 뿐만 아니라 select, textarea 등 모든 입력 태그에 사용
   ```html
   <input type="date" disabled>
   <input type="checkbox" checked disabled>
   <input type="password" value="password" disabled>
   ```   
   <input type="date" disabled>
   <input type="checkbox" checked disabled>
   <input type="password" value="password" disabled>
   
   5)readonly   
   읽기만 가능합니다. disabled와 외관상으로는 차이가 없음.   
   input 뿐만 아니라 select, textarea 등 모든 입력 태그에 사용
   ```html
      <input type="date" readonly>
      <input type="checkbox" checked readonly>    
      <input type="password" value="password" readonly>
   ```   
   <input type="date" readonly>
   <input type="checkbox" checked readonly>
   <input type="password" value="password" readonly>

1. # 폼 요소의 종류
   <a href="#text">`<input type="text|password">`</a>   
   <a href="#inputButton">`<input type="button|submit|reset|image">`</a>   
   <a href="#checkradio">`<input type="checkbox|radio">`</a>   
   <a href="#select">`<select>`</a>, <a href="textarea">`<textarea>`</a>   
   <a href="#button">`<button type="button|reset|submit">`</a>   
   <a href="#label">`<label>`</a>   

   폼 요소는 전부 name과 id와 value를 가지고 있는데 name이 서버 쪽에서 받을 수 있는 요소들의 identity가 되고, id는 html에서 구분하는 역할이며 value는 서버 쪽에서 name으로 요소를 구분 후 가져오는 값이 됩니다.   
   text, password, button, submit, reset, image는 서버 쪽에서 name으로 구분하며 해당 요소의 값은 value로 받습니다.   
   checkbox와 radio와 select도 같은 카테고리를 name으로 구분합니다.   

1. # <span id="text">텍스트 입력 text와 password</span>
   이름이나 주소 등 한 줄 텍스트를 입력받을 땐 text를 사용하고, 특별히 암호를 입력 받을 땐 password 속성를 사용합니다.   

   type="text|password"   
   name="요소 이름"   
   maxlength="문자 개수"   
   size="입력 창의 크기"   
   value="초기 텍스트"

   ```html
      <input type="text" name="name" maxlength="10" size="10" value="이 글을 지우고 이름을 입력하세요">
   ```   
   <input type="text" name="name" maxlength="10" size="10" value="이 글을 지우고 이름을 입력하세요">   

   passwor를 사용하는 경우 입력 값이 *로 입력되어 알 수 없게 됩니다.   
   ```html
      <input type="password" name="pwd" maxlength="10" size="10" value="이 글을 지우고 암호를 입력하세요">
   ```
   <input type="password" name="pwd" maxlength="10" size="10">   

1. # <span id="textarea">textarea</span>
   한 줄을 입력 받을 땐 input type=text를 사용하고 여러 줄을 입력 받을 땐 textarea를 사용하게 됩니다.   

   cols="열 개수"   
   rows="행 개수"   
   name="요소 이름"   
   wrap="자동 줄바꿈 off|hard|soft"   
   *hard : 한 줄 전체를 줄바꿈   
   soft : 한 칸을 띄움   

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="NWmRRoE" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/NWmRRoE">
   Untitled</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

   영어 기준 가로 10글자, 세로 5글자의 박스 크기를 만듭니다. 세로 크기는 최초 설정이고 글자 수가 늘어나면 세로 글자 수 크기도 늘어납니다.   
   hard옵션은 띄워쓰기하는 부분부터 전체를 줄 바꿈하고, soft옵션은 한칸만 띄워쓰게 됩니다.   

1. # datalist
   네이버 검색 창에서 검색할 때 추천 검색목록이 나타납니다. `<input type="text">` 밑에 datalist태그를 추가해서 만들 수 있습니다. input의 속성 list와 datalit의 id가 동일 해야 합니다.

   <p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="PogGGOO" data-user="khj99" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
   <span>See the Pen <a href="https://codepen.io/khj99/pen/PogGGOO">
   Untitled</a> by kimhyunjin (<a href="https://codepen.io/khj99">@khj99</a>)
   on <a href="https://codepen.io">CodePen</a>.</span>
   </p>
   <script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

1. # <span id="inputButton">input으로 버튼 만들기</span>
   
   type="button|submit|reset|image"   
   name="서버에서 받을 버튼 이름"   
   value="버튼 보여지는 문자열"   
   src="이미지url"   

   *input은 닫는 태그가 없기 때문에 `<input type="button">버튼을 누르세요</input>` 이런 식으로 사용하지 않음. value로 버튼에 보여지는 문자열 출력   
   src에 이미지를 넣으면 버튼에 이미지가 출력됩니다.   

   ```html
      <input type="button" name="general_btn" value="일반 버튼">
      <input type="submit" name="submit_btn" value="전송"> <!-- 서버쪽으로 form 데이터를 전송 -->
      <input type="reset" name="reset_btn" value="다시 입력"> <!-- 폼에 입력된 내용을 지우고 초기화 -->
      <input type="image" name="img" src="../../imgs/CH/sunset.png" style="width:100px;height:50px"> <!-- 이미지 입력 -->
   ```   
   <input type="button" name="general_btn" value="일반 버튼"><br>
   <input type="submit" name="submit_btn" value="전송"><br>
   <input type="reset" name="reset_btn" value="다시 입력"><br>
   <input type="image" name="img" src="../../imgs/CH/sunset.png" style="width:100px;height:50px"><br>

1. # <span id="button">button으로 버튼 만들기</span>

   type="button|submit|reset"   
   name="서버에서 받을 버튼 이름"   
   value="임시 데이터"

   *button태그는 닫는 태그가 있기 때문에 input 태그처럼 value 속성에 보여지는 문자열을 입력하지 않고 `<button>버튼에 보여지는 문자열</button>`이런 식으로 닫는 태그 안에 버튼에 보여지는 문자열을 입력합니다.   
   value에는 임시 데이터를 저장해서 사용할 수 있습니다.   
   submit과 reset의 기능은 위에 input type="button"과 동일합니다.   

   ```html
      <button type="button" name="general_btn">일반 버튼</button>
      <button type="submit" name="submit_btn">전송</button> <!-- 서버쪽으로 form 데이터를 전송 -->
      <button type="reset" name="reset_btn">다시 입력</button> <!-- 폼에 입력된 내용을 지우고 초기화 -->
      <button type="button" name="img"><img src="../../imgs/CH/sunset.png" style="width:100px;height:50px"></button> <!-- 이미지 입력 -->
   ```   
   <button type="button" name="general_btn">일반 버튼</button>   
   <br>
   <button type="submit" name="submit_btn">전송</button>   
   <br>
   <button type="reset" name="reset_btn">다시 입력</button>   
   <br>
   <button type="button" name="img"><img src="../../imgs/CH/sunset.png" style="width:100px;height:50px"></button>
   
   `<button type="reset"><img src=".."></button>`과 같이 submit이나 reset도 이미지 버튼을 만들 수 있습니다.   

   *`<button>`의 기본 타입은 submit입니다. 그렇기 때문에 일반 버튼으로 사용하려면 type="button"을 명식해줘야 합니다. form 밖에서는 상관없습니다.   

1. # <span id="checkradio">check박스와 radio박스</span>

   type="checkbox|radio"   
   name="요소 이름"으로 그룹 지정   
   value="서버에 넘겨줄 선택된 값"   
   checked   

   *checked 이 속성이 있으면 초기에 선택 상태가 됩니다.   

   1)체크 박스   
   다중 선택이 가능합니다.   

   ```html
      <input type="checkbox" name="subject" value="math">수학
      <input type="checkbox" name="subject" value="eng">영어
      <input type="checkbox" name="subject" value="physics">물리
      <input type="checkbox" name="hobby" value="running">달리기
      <input type="checkbox" name="hobby" value="swimming">수영
   ```   
   <input type="checkbox" name="subject" value="math">수학
   <input type="checkbox" name="subject" value="eng">영어
   <input type="checkbox" name="subject" value="physics">물리
   <input type="checkbox" name="hobby" value="running">달리기
   <input type="checkbox" name="hobby" value="swimming">수영
   <br>   
   
   다중 선택이 가능하기 때문에 그룹을 묶을 필요가 없지만 서버 쪽에서 받을 때 카테고리 별로 나누기 위해서 name설정   
   수학에 checked옵션이 있기 때문에 최초 선택된 상태로 출력됩니다.   

   2)라디오 버튼   
   여러 값 중 1개의 값만 선택을 합니다.   
   name으로 같은 그룹을 묶게됩니다.   

   ```html
      <input type="radio" name="subject" value="math" checked>수학
      <input type="radio" name="subject" value="eng">영어
      <br>
      <input type="radio" name="fruit" value="banana" checked>바나나
      <input type="radio" name="fruit" value="apple">사과
   ```
   <input type="radio" name="subject" value="math" checked>수학
   <input type="radio" name="subject" value="eng">영어
   <br>
   <input type="radio" name="fruit" value="banana" checked>바나나
   <input type="radio" name="fruit" value="apple">사과

   checked 속성이 있는 수학과 바나나가 최초 선택된 상태입니다.   

1. # <span id="select">select</span>

   name="요소 이름"   
   size="개수"   
   multiple="다중 선택"  
   *size는 최초 보이는 항목의 갯수로 디폴트는 1입니다.   
   multiple속성을 적으면

   option태그 속성   
   value="항목이 선택되었을 때 서버로 넘겨주는 값"   
   selected="초기에 선택 될 항목"   

   `<select>`태그로 감싸고 내부에 `<option>`태그로 항목을 나열합니다.   

   ```html
      <select name="state">
         <option value="kor">한국어
         <option value="eng">영어
         <option value="china">중국어
      </select>
      <select name="number">
         <option value="kor">82
         <option value="eng">1
         <option value="china">86
      </select>
   ```   

      <select name="state">   
         <option value="kor">한국어   
         <option value="eng">영어   
         <option value="china">중국어   
      </select>   

      <select name="number">   
         <option value="kor">82   
         <option value="eng">1   
         <option value="china">86   
      </select>   

   *마지막에 항목에 `/select`가 생기는 건 마크업 파일이 태그를 제대로 인식 못 하기 때문   
   서버에서 데이터를 받을 땐 name으로 구분 후 value 값들인 kor, eng, china를 받게 됩니다.   

   *datalist와 select의 차이점   
   `<datalist>`를 사용하면 옵션 리스트에서 선택할 수도 있고 입력창에 직접 입력하여 항목을 선택할 수 있지만, `<select>`의 경우 옵션 리스트에서만 선택할 수 있습니다.   

1. # <span id="label">label</span>
   input 태그를 설명해주는 메세지를 추가합니다. label대신 span을 사용해도 기능과 시각적으로는 차이가 없습니다. 하지만 input 태그 설명의 용도로 개발이 되었기 때문에 웹 접근성을 향상시키기 위해 label을 사용할 것을 권장하고 있습니다.   

   label사용 방법에는 2가지가 있습니다.   

   1)label로 폼 요소 둘러싸기
   ```html
      <label>
         이름 : <input type="text">
      </label>
   ```   
   <label>
      이름 : <input type="text">
   </label>

   2)for속성과 id로 연결
   ```html
      <label for="myname">이름 : </label>
      <input type="text" id="myname">
   ```   
   <label for="myname">이름 : </label><input type="text" id="myname">
   label태그에 for속성과 input 폼 요소의 id가 일치해야 합니다.

1. # 형식을 가진 텍스트 입력
   1)password
   비밀번호를 입력 양식이 됩니다.   
   ```html
      <input type="password">
   ```   
   <input type="password">   

   2)email   
   일반 input 박스와 다를 게 없어 보이지만 모바일 환경으로 바뀌면 제공되는 키패드가 이메일 전용이 됩니다.   
   ```html
      <input type="email" placeholder="name@domain">
   ```   
   <input type="email" placeholder="name@domain" >   
   type이 email이면 형식이 맞는지 유효성 검사를 하게 됩니다.   

1. # 기타 태그들 
   1)색 선택 태그
   색을 선택할 수 있는 컬러 피커가 나타납니다.   
   ```html
      <input type="color">
   ```   
   <input type="color" style="width:100px;height:30px">   
   
   2)date   
   달력 데이터 피커가 나타납니다.   
   ```html
      <input type="date" value="2024-03-16">
   ```   
   <input type="date" value="2024-03-16" style="width:200px;height:30px">   

   3)datetime-local   
   날짜와 시간이 나타납니다.   
   ```html
      <input type="datetime-local" value="2024-03-16T21:32:30">
   ```   
   <input type="datetime-local"  value="2024-03-16T21:32:30" style="width:500px;height:30px">  
   
   3)file   
   파일을 선택할 수 있습니다.   
   ```html
      <input type="file">
   ```   
   <input type="file">   
   ```html
         <input type="file" multiple> //파일 다중 선택 가능
   ```   
   multiple옵션 사용 : <input type="file" multiple>   




         





  