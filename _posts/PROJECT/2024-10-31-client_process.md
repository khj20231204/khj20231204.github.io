---
layout: single
title: 클라이언트 부분 실행 순서
categories: PROJECT
tag: []
author_profile: false
---   

1. # async 메소드 위치
   apis에서 api.js와 auth.js가 있는데 api.js에서 axios를 생성한다. axios 한번의 생성으로 회원가입 부분 다 처리.   
   auth.js에서 직접 서버로 요청하는 post, get, put을 처리한다.   

   auth.js
   ```javascript
      //로그인
      export const login = (username, password) => api.post(`/login?username=${username}&password=${password}`);

      //사용자 정보
      export const info = () => api.get(`/users/info`); 

      //회원가입
      export const join = (data) => api.post(`/users/join`, data)

      //회원정보 수정
      export const update = (data) => api.put(`users/update`, data);

      //회원탈퇴
      export const remove = (userId) => api.delete(`/users/${userId}`)
   ```
   axios를 사용하는 __함수__ 로만 이루어진 파일   

   LoginContextProvider.js
   ```javascript
      1)const login = async(username, password) => {
         ...
         response = await auth.info();
         ...
      }   

      2)const loginCheck = async () => {
         ...
         const response = await auth.login(username, password);
         ...
      }
   ```

1. #  LoginContextProvider의 실행 순서

   로그인버튼을 클릭

   1)const login = async(username, password) => {...}   

   2)const loginCheck = async () => { ... }

   3)const loginSetting = (userData, accessToken) => { ... }

   4)const logoutSetting = () => { ... }

1. # const login = async(username, password) => {...}

   __토큰을 쿠키에 저장__   

   아이디와 패스워드를 입력 후 서버쪽에서 인증이 되면 jwt토큰을 생성하여 await의 위치로 돌려줌 여기서부터 시작 =>   

   토큰을 잘라내서 쿠키에 저장 이후 loginCheck 호출   

   ```javascript
      const response = await auth.login(username, password);
   ```
   <img src="../../imgs/project/client_processing_1.png" style="border:3px solid black;border-radius:9px;width:700px">    
   response에는 data, status, headers 등의 값을 가지고 있다   
   headers에서 토큰을 잘라낸다   
   status가 200이면 성공적으로 데이터를 받은 것이 된다.   

   status가 200이면 잘라낸 jwt를 쿠키에 저장한다   

   loginCheck()로 넘어간다

1. # const loginCheck = async () => { ... }
   
   __토큰을 서버로 보내 클라이언트 정보 가져오기__   

   클라이언트이 토큰을 http header부분에 실어서 다시 서버로 보내고, 서버에서는 해당 사용자의 정보를 받아온다

   헤더에 토큰 저장
   ```javascript
      api.defaults.headers.common.Authorization = `Bearer ${accessToken}`
   ```

   서버로부터 값 가져오기   
   ```javascript
      let response = await auth.info();
      console.log(response);
      
      let data = response.data;
      console.log(data);
   ```

   response 응답 값  
   ```json
      Object
      config : {transitional: {…}, adapter: Array(3), transformRequest: Array(1), transformResponse: Array(1), timeout: 0, …}
      data : {no: 8, userId: 'user', userPw: null, userPwCheck: null, name: 'testname', …}
      headers : AxiosHeaders {access-control-allow-headers: '*', access-control-allow-methods: '*', access-control-allow-origin: '*', cache-control: 'no-cache, no-store, max-age=0, must-revalidate', connection: 'close', …}
      request : XMLHttpRequest {onreadystatechange: null, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}
      status : 200
      statusText : "OK"
      [[Prototype]] : Object
   ```

   data 응답 값   
   ```json
      Object
      authList : Array(2)
      0 : {authNo: 0, userId: 'user', auth: 'ROLE_USER'}
      1 : {authNo: 0, userId: 'user', auth: 'USER'}
      length : 2 
      [[Prototype]] : Array(0)
      email : "testemail@mail.com"
      enabled : 0
      name : "testname"
      no : 8
      regDate : null
      updDate : null
      userId : "user"
      userPw : null
      userPwCheck : null
      [[Prototype]] : Object
   ```

1. #  const loginSetting = (userData, accessToken) => { ... }

   __사용자 정보를 전부 state에 저장__   

   ```javascript
      api.defaults.headers.common.Authorization = `Bearer ${accessToken}`;

      setLogin(true);

      const updateUserInfo = {no, userId, roleList};
      setUserInfo(updateUserInfo);

      const updateRoles = {isUser : false, isAdmin : false}

      roleList.forEach((role) => {
         if(role === 'ROLE_USER') updateRoles.isUser = true;
         if(role === 'ROLE_ADMIN') updateRoles.isAdmin = true; 
      });

      setRoles(updateRoles);
   ```
   토큰을 헤더에 저장   
   로그인 유무   
   유저 정보 세팅   
   권한 정보 세팅   

1. # 회원가입🎇
   pages/Join.jsx ➡️ join/joinFormJS.jsx ➡️ LoginJoin/SignUp.jsx (LoginJoin에 컴포넌트로 SignIn, SignUp, OverlayContainer가 있는데 회원가입에 필요한 건 SignUp 컴포넌트만 필요하기 때문에 SignUp만 남기도 나머지는 다 지운다)  

   ```javascript
      -Join.jsx-

      import * as auth from '../apis/auth' //auth import

      const join = async(form) => { ... }

      return (
         <>
            <Header/>
            <div className='container'>
               <JoinFormJS join={join}/> //JoinFormJS로 join함수를 props로 전달
            </div>
         </>
      );
   ```

   ```javascript
      -JoinFormJS.jsx-

      const JoinFormJs = ({join}) => { ... } //앞에서 props로 전달한 join을 받는다

      return (
         <div className="joinformjs">
            <div className="wrapper">
               <div className="container right-panel-active">
                  <SignUp join={join}/> //JoinFormJs에서는 join을 전달만 함
                  <SignIn/>
                  <OverlayContainer/>
               </div>
            </div>
         </div>
      );
   ```

   ```javascript
      -SignUp.jsx-

      <form onSubmit={(e)=>onJoin(e)}> //3️⃣폼의 onSubmit이 실행
         ...
         <button type="submit" className="form_btn">Sign Up</button>  //2️⃣버튼을 클릭
         ...
      </form>

      const SignUp = ({join}) => { //1️⃣JoinFormJS에서 props로 전달 받은 join함수를 받음

         const onJoin = (e) => { //4️⃣onJoin함수 실행
            e.preventDefault();

            const form = e.target;

            const userId = form.username.value;
            const userPw = form.password.value;
            const email = form.email.value;

            join({userId, userPw, email}) //폼의 정보를 join함수의 매개변수로 전달하고 join함수를 호출
         }
      }

   ```

1. # 회원정보 수정💡
   pages/User.jsx ➡️ components/UserForm.jsx   

   컴포넌트는 다른 페이지에서 사용할 수 있기 때문에 state설정이나 함수 설정은 pages에서 수행. 컴포넌트는 값만 넘겨받는 기능만 수행   

   부모 컴포넌트에서 자식 컴포넌트로 props전달이 가능하지만, 자식 컴포넌트에서는 부모 컴포넌트로 porps를 전달할 수 없다. 그렇지만 함수로 호출은 가능한다.  

   User.jsx에서는 회원 정보 조회, 회원 정보 수정, 회원 탈퇴 기능을 수행한다.   
   

   
