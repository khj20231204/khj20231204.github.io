---
layout: single
title: 이슈 정리
categories: PROJECT
tag: []
author_profile: false
---   

1. # 에러 번호
   401 Unauthorized - 인증 실패   
   403 Forbidden - 접근 거부(권한 없음)   
   404 Not Found   

1. # 부트스트랩의 href를 link로 변경

1. # 자바스크립트 사용하기

   ```
      Cannot read properties of null (reading 'addEventListener')
      TypeError: Cannot read properties of null (reading 'addEventListener')
         at __webpack_modules__../src/LoginForm.js.window.onload (http://localhost:3000/static/js/bundle.js:214:13)
   ```

   css의 class를 className으로 변경   
   css앞에 전부 loginformjs 붙이기    
   const container = document.querySelector(".loginformjs .container");
   "container" 값이 헤더의 container값을 가져왔다   

   

   window.onload 사용
   ```
      window.onload = function(){

      const signUpBtn = document.getElementById("signUp");
      const signInBtn = document.getElementById("signIn");
      const container = document.querySelector(".container");

         signUpBtn.addEventListener("click", () => {
            alert("df");
         container.classList.add("right-panel-active");
         
         });
         
         signInBtn.addEventListener("click", () => {
         alert("geg");
         container.classList.remove("right-panel-active");
         });
      } 
   ```

   script async로 삽입
   ```
      <div id="root"></div>
    <!-- js파일 삽입-->
    <!-- <script async src="assets/js/LoginForm.js"></script> -->

   ```

   이벤트는 3가지의 중심 요소가 존재한다.  어떤 이벤트를 발생시킬 것인지의 이벤트event, 이벤트가 발생하면 실행되게 할 함수 event handler, 그리고 이벤트와 함수를 연결하는 addEventListener가 있다 addEventListener(event, handler, useCapture); addEventListener는 이벤트와 핸들러를 연결짓는 함수이다
   *useCapture: (선택 사항) 이벤트 버블링과 캡처링 중 어떤 방식으로 이벤트를 처리할지 결정하는 boolean 값

   1. # 클라이언트의 username과 password가 null이 뜬다

      1)처음 연결 오류 poroxy 설정   
      <img src="../../imgs/project/axios_error_2.png" style="border:3px solid black;border-radius:9px;width:700px">   
      클라이언트와 서버의 포트 번호 설정이 이루어지지 않았다 proxy에 대해서 조사해서 쓰기   

      package.json   
      ```json
            "development": [
            "last 1 chrome version",
            "last 1 firefox version",
            "last 1 safari version"
         ]
      },
      "proxy": "http://localhost:8088" //추가
      }
       ```   

      2)오류   
      클라이언트 오류 표시   
       <img src="../../imgs/project/axios_error_1.png" style="border:3px solid black;border-radius:9px;width:700px">    

      ```
         2024-10-30T19:29:50.222+09:00  INFO 26064 --- [server] [nio-8088-exec-4] c.h.s.s.j.f.JwtAuthenticationFilter      : JwtAuthenticationFilter username : null
         2024-10-30T19:29:50.223+09:00  INFO 26064 --- [server] [nio-8088-exec-4] c.h.s.s.j.f.JwtAuthenticationFilter      : JwtAuthenticationFilter password : null
      ```
      클라이언트와 서버를 하나의 vscode에서 같이 실행 시키니깐 값은 받아온다   

      3)
      클라이언트 오류 표시   
      ```
         headers.replace is not a function
         TypeError: headers.replace is not a function
            at login (http://localhost:3000/static/js/bundle.js:1827:33)
      ```   
      <img src="../../imgs/project/axios_error_3.png" style="border:3px solid black;border-radius:9px;width:300px">    

      <img src="../../imgs/project/chrome_network.png" style="border:3px solid black;border-radius:9px;width:700px">   

      ```java
         const data = response.data;   
         const status = response.status;  
         const headers = response.headers; 
         
         const authorization = headers.authorization;  //headers의 authorization
         const accessToken = authorization.replace("Bearer ", ""); //authorization에서 replace, Bearer 다음 한칸 뛰오고 
      ```   

1. # axios오류

   <img src="../../imgs/project/axios_error_4.png" style="border:3px solid black;border-radius:9px;width:300px">    

   async로 요청을 보냈는데 받는 과정에서 error 발생   
   server는 정상 가동 중   
   ```javascript
      response = await auth.info(); //await로 받는 과정에서 에러발생

      console창에 오류 메세지:
      GET http://localhost:3000/users/info 403 (Forbidden)
      AxiosError {message: 'Request failed with status code 403', name: 'AxiosError', code: 'ERR_BAD_REQUEST', config: {…}, request: XMLHttpRequest, …}
      */
   ```

   1)CORS로 접근

   2)다시 에러 문구 분석 
   403 (Forbidden) 에러에 대한 설명
   403 (Forbidden) 에러는 웹 서버가 사용자의 요청을 이해했지만, 해당 리소스에 대한 접근 권한이 없다고 알려주는 HTTP 상태 코드입니다. 마치 문이 잠겨 있어 들어갈 수 없다는 뜻과 같습니다.   
   ```java
      //@Secured("ROLE_USER") //USER 권한 설정 <-- 권한을 변경해봤다
      @GetMapping("/info")
      public ResponseEntity<?> userInfo(@AuthenticationPrincipal CustomUser customUser) { ... }
   ```
   클라이언트에서 id와 pass입력 후 login버튼 클릭 -> 서버 측에서 id와 pass 확인 후 토큰 생성 -> 토큰에 사용자 정보를 담아서 클라이언트에 전송 -> 클라이언트가 받는 건 암호화된 토큰 -> info요청시 이 토큰을 다시 서버측에 전달 -> 서버에서 비밀키를 이용해서 토큰 디코딩 해석 후 아이디와 권한 등 정보를 활용.   
   즉, 클라이언트 측이 가지고 있는 토큰으로는 권한 정보를 확인 불가능.   
   서버측에서 토큰을 받아서 해석한 값에 권한을 확인해봐야함   


   UserAuth.java에서 map형태로 id와 권한 설정   
   UserServiceImpl.java의 insert에서 권한 등록   
   JwtTokenProvider.java의 createToken에서 토큰 생성   
   login시 받은 토큰을 해석하여 권한을 확인   
   CustomerUser.java의 getAuthorities에서 권한을 가져온다

   데이터베이스에 ROLE_USER가 USER로 등록되어있는 걸 발견   


1. # CORS   
   교차 출처 리소스 공유 (Cross-origin Resource Sharing, Cors)는 추가 HTTP헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 
   쉽게 말해서 도메인,프로토콜,포트번호가 하나라도 다를 경우에 출처가 다른 교차
   출처(Cross Origin)라고 판단되며 브라우저에서는 보안 때문에 Cross-Origin HTTP 
   요청을 제한한다. 권한을 부여 받기 위한 Cross-Origin 요청은 서버에서 허가를
   받아야 한다.

   교차 출처 리소스 공유 (Cross-origin Resource Sharing, Cors)는 추가 HTTP헤더를
사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에
접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다. 
쉽게 말해서 도메인,프로토콜,포트번호가 하나라도 다를 경우에 출처가 다른 교차
출처(Cross Origin)라고 판단되며 브라우저에서는 보안 때문에 Cross-Origin HTTP 
요청을 제한한다. 권한을 부여 받기 위한 Cross-Origin 요청은 서버에서 허가를
받아야 한다.

 1)React CORS문제 해결하기 :   
   클래스나 메소드 위에 @CrossOrigin 어노테이션을 추가한다.   
   ```java
      @RestController
      @CrossOrigin("*")  //<-- 추가
      public class HomeController {
         @RequestMapping("/sample")
         
         public SampleVo sample() {
            SampleVo sv = new SampleVo();
            sv.setMno(23);
            sv.setFirstName("홍");
            sv.setLastName("길동");
            return sv;
         }
      }
   ```

   2)React CORS문제 해결하기 : 
   WebConfig 클래스 생성해서 react의 3000번 포트허용
   ```java
      @Configuration
      public class WebConfig implements WebMvcConfigurer{
      
      @Override
      public void addCorsMappings(CorsRegistry registry) {
         registry.addMapping("/**") // react의 3000번 포트 허용
         .allowedOrigins("http://localhost:3000") 
         .allowedMethods("GET", "POST", "PUT","DELETE")
         .allowedHeaders("*")
         .maxAge(3600);
      }
   }
   ```
         
1. # context 바인딩 에러

   <img src="../../imgs/project/context_binding_error.png" style="border:3px solid black;border-radius:9px;width:300px">    

   ```javascript  
      -LoginContextProvider.jsx-

      export const LoginContext = createContext();

      const LoginContextProvider = ({ children }) => { ... }

      export default LoginContextProvider;
   ```
   LoginContextProvider 컴포넌트에서 LoginContextProvider는 default로 export가 되고 createContext()로 선언된 LoginContext를 자식 컴포넌트에서 가져다가 사용하게 된다. export를 할 때 default가 아닌 경우 이름을 변경하면 인식을 못 한다.   

   ```javascript  
      -admin.jsx-

      import {LoginContextProvider} from '../contexts/LoginContextProvider'; //error발생
      import LoginContextProvider from '../contexts/LoginContextProvider'; //문법에는 이상이 없지만 isLogin, roles를 인식 못 함
      import LoginContext from '../contexts/LoginContextProvider'; //error발생, default 이외에는 { }를 감싸야함
      import {LoginContextSe} from '../contexts/LoginContextProvider'; //error발생, 이름 변경
      import {LoginContext} from '../contexts/LoginContextProvider'; //error발생, 정상 작동


      const Admin = () => {
         ...
         const { isLogin, roles } = useContext(LoginContext)
         ...
      }
   ```

1. # list requestMapping 403오류

    <img src="../../imgs/project/list_mapping_403.png" style="border:3px solid black;border-radius:9px;width:800px">

    <img src="../../imgs/project/list_mapping_403_2.png" style="border:3px solid black;border-radius:9px;width:800px">

   오류 메세지
   ```   
      Board.jsx:57 
      GET http://localhost:8088/board/list?page=2 403 (Forbidden)
      Board.jsx:62 
      AxiosError {message: 'Request failed with status code 403', name: 'AxiosError', code: 'ERR_BAD_REQUEST', config: {…}, request: XMLHttpRequest, …}
      code :  "ERR_BAD_REQUEST"
      config :  {transitional: {…}, adapter: Array(3), transformRequest: Array(1), transformResponse: Array(1), timeout: 0, …}
      message : "Request failed with status code 403"
      name : "AxiosError"
      request : XMLHttpRequest {onreadystatechange: null, readyState: 4, timeout: 0, withCredentials: false, upload: XMLHttpRequestUpload, …}
      response : {data: '', status: 403, statusText: '', headers: AxiosHeaders, config: {…}, …}
      status : 403
      stack : "AxiosError: Request failed with status code 403\n    at settle (http://localhost:3000/static/js/bundle.js:75177:12)\n    at XMLHttpRequest.onloadend (http://localhost:3000/static/js/bundle.js:73828:66)\n    at Axios.request (http://localhost:3000/static/js/bundle.js:74327:41)"
      [[Prototype]] : Error
   ```

   https://velog.io/@jhbae0420/%EB%BD%80%EB%AA%A8%EB%8F%84%EB%A1%9C-%EB%A9%94%EC%9D%B4%ED%8A%B8-%EC%8A%A4%ED%94%84%EB%A7%81-%EC%8B%9C%ED%81%90%EB%A6%AC%ED%8B%B0%EC%9D%98-CSRF-%ED%95%84%ED%84%B0-%ED%95%B4%EC%A0%9C%EB%A5%BC-%ED%86%B5%ED%95%9C-403-Forbidden-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0

   csrf참고 -> 아니였다

   SecurityConfig.java에서 인가 설정 -> 해줬는데 반복

   인가부분이 아니라 파라미터값이 달라도 에러가 발생한다는 것을 알았다

   ```
       fetch('http://localhost:8088/board/list')
         .then((res) => {
            console.log(1, res)
      });
   ```
   사용 허용

   ```
      axios.get('http://localhost:8088/board/list')
         .then(response => {
           console.log(response.data);
         })
         .catch(error => {
           console.error(error);
         });
   ```
   허용 불가

   무엇이가 이상하다고 생각, 잠시 쉬고 왔더니 되었다

   cors를 webConfig로 차단
   ```
      @Configuration
      public class WebConfig implements WebMvcConfigurer {
         
         @Override
         public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/**") // react의 3000번 포트 허용
            .allowedOrigins("http://localhost:3000") 
            .allowedMethods("GET", "POST", "PUT","DELETE")
            .allowedHeaders("*")
            .maxAge(3600);
            }
         }
   ```
   아니였다

   post로 전송
   ```java
       @PostMapping("/list")
      //public ResponseEntity<Map<String, Object>> list() throws Exception {
      //public ResponseEntity<Map<String, Object>> list(@RequestParam(value="page", defaultValue="1") int page) throws Exception {
      public ResponseEntity<Map<String, Object>> list(@RequestParam(value="page", defaultValue="1") int page, @RequestBody Board board) throws Exception {
         ...
      }

      axios.post('http://localhost:8088/board/list?page=2', board)
         .then(response => {
           console.log(response.data);
         })
         .catch(error => {
           console.error(error);
         });
   ```
   오류가 나지 않음

   get으로 전송   
   ```java
       @GetMapping("/list")
      public ResponseEntity<Map<String, Object>> list(@RequestParam(value="page", defaultValue="1") int page, @RequestBody Board board) throws Exception {
         ...
      }

      axios.get('http://localhost:8088/board/list?page=2', board)
         .then(response => {
           console.log(response.data);
         })
         .catch(error => {
           console.error(error);
         });
   ```
   에러 발생

1. # client - 호출하지 않은 함수를 계속 읽어 올 때
   
   ```javascript
       <button onClick={() => {deleteUser(userInfo.userId)}}>Delete Account</button>
   ```   
   1)type="button"이 없다. submit으로 설정되어 졌다
   2)deleteUser(userInfo.userId)는 부모로 받은 함수기 때문에 
   ```javascript
       <button type="button" onClick={deleteUser(userInfo.userId)}>Delete Account</button>
   ```
   다음과 같이 바인딩 시키지 않고 함수 안에 호출해야 한다. 

1. # context 사용시 출력값 지연
      useEffect()의 의존성 배열에 state값을 입력   

      A와 B는 한페이지에 선언된 컴포넌트들   
      A에 useContext를 가져옴   
      B에서 값을 변경만함   
      A의 useEffect의 의존성 배열에서 이를 탐지 적용함   

1. # Warning: A component is changing an uncontrolled input to be controlled. 
   
   에러 메시지
   ```
       A component is changing an uncontrolled input to be controlled. This is likely caused by the value changing from undefined to a defined value, which should not happen. Decide between using a controlled or uncontrolled input element for the lifetime of the component.
   ```   

   page 디렉토리에 있는 부모 컴포넌트   
   ```javascript
      - WriteBoard.jsx -

      <WriteBoardForm userId={userId}/>
   ```

   component 디렉토리에 있는 자식 컴포넌트   
   ```javascript
      - WriteBoardForm.jsx -

      const WriteBoardForm = (props) => {
         const {userId} = props;
         ...
         {{backgroundColor:'whitesmoke'}} value={userId}/>
         ...
      }
   ```

   글쓰기를 할 때 부모 컴포넌트에서 자식 컴포넌트로 userId를 넘겼는데 취소를 누를 경우 navigate(-1)를 사용하여 되돌아 갔다가 다시 글쓰기로 넘어오면서 발생하는 에러   

   컴포넌트는 새로고침되거나 재런딩되면 기존의 값은 초기화 되기 때문에 부모 컴포넌트로부터 props로 userId를 받았는데 이것이 없어지기 때문.   

   해결 : props로 전달하지 말고 userId는 메인에서 로그인 할 때 받기 때문에 이때 context로 저장한다. useState를 선언 후 useEffect에 등록한다.   

   ```javascript
      import { LoginContext } from '../../contexts/LoginContextProvider';

      let {userInfo} = useContext(LoginContext); //context에서 userInfo정보를 가져와서
      let [userId, setUserId] = useState(userInfo.userId);

      useEffect(() => {
         setUserId(userInfo.userid);
      }, [userId])
   ```

   아니였다. context는 변수들의 상태를 저장하는 도구이며, 새로고침하면 역시 기존의 내용이 없어진다. 값을 저장하기 위해서는 다른 저장소가 필요하다.   

   1. 로컬 스토리지 사용하기   
   2. 쿠키 사용 or 서버측에서 관리하기   

   현재는 서버가 없기 때문에 간단하게 로컬 스토리지에 저장할 수 한다.   
   ```javascript
      //일반 값 저장하기와 불러오기
      localStorage.setItem('access', access);   //파싱없이 그냥 저장
      const accessToken = localStorage.getItem('access'); //파싱없이 그냥 불러옴
      
      //객체 저장하기와 불러오기
      localStorage.setItem('userInfo', JSON.stringify(userInfo)); //userInfo객체를 파싱하여 로컬 스토리지에 저장
      const userId = JSON.parse(localStorage.getItem('userInfo')).userId; //userInfo객체에서 userId란 이름의 값을 가져와서 파싱해서 userId 변수에 저장
   
      //삭제
      localStorage.removeItem('userId');

      //clear
      localStorage.clear();
   ```
   <span style="color:red">객체를 저장하고 불러올 때만 parsing을 한다</span>