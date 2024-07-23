---
layout: single
title: REACT 최초 설정
categories: REACT
tag: [React,설치]
---

* windows의 경우 PowerShell 보다는 cmd창에서 작업하는 것을 권장합니다.
  PowerShell의 경우 Windows 기본 환경 값이 Restricted로 되어있어 스크립트의 직접 실행을 막아놨습니다. 그래서 PowerShell에서 밑에 명령어들을 실행하기 위해선 execution policy을 변경해야 됩니다.(간단하지만 귀찮아서..)   
  <br>
1. # node.js설치
   node.js 검색 후 홈페이지 들어가서 안정적인 LTS를 다운받으시면 됩니다.   
   <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/node_lts.jpg">
1. # react 폴더생성
   폴더를 생성 후 경로창에 바로 cmd를 입력해서 해당 경로를 가진 cmd를 실행합니다.   
   <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/react_make_folder.jpg">   
   C:\react 폴더에서 cmd를 바로 입력합니다.   
   <br>
   <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/path_cmdwindow.jpg">   
   cmd창 경로가 C:\react>로 나타납니다.
1. # node 버전 확인
   node -v
1. # npx로 cra설치하기
   my-app이란 이름을 가진 프로젝트를 만들기위해 npx에서 cra라이브러리를 이용합니다.   
   npx create-react-app my-app    
   <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/cmd_make_app.jpg"><br>
      <h4>■다음과 같은 에러가 뜨는 경우..</h4>
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/create_react_app_error.png">   
      <h5>원인</h5>
      C:\Users\{사용자 폴더}\AppData\Roaming에 npm 폴더가 없기 때문입니다. 
      <h6>AppData폴더란?</h6>
      윈도우 어플리케이션의 설정 파일들이나 임시 저장파일들, 동기화를 위한 데이터를 저장하는 곳입니다. 폴더는 Local, LocalLow, Roaming 3개로 구성되어 있습니다.      
      <h5>해결책</h5>
      npm install npm -g 입력 후 다시 설치   
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/create_react_app_solve.png">   
      npm install [패키지명] [옵션]    
      g 옵션을 붙일 경우 시스템 폴더(Roaming)에 설치를 하는데 npm 패키지를 직접 설치하게 됩니다.   
1. # 설치 완료 화면   
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/make_app_complete.jpg">   
1. # npm 실행하기   
      반드시 프로젝트 해당 폴더에서 npm start를 입력해야 됩니다.   
      <img style="border: 3px solid black;border-radius:9px;" src="../../imgs/react/app_path.jpg">      
      경로my-app을 확인합니다.<br><br>
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/npm_browser_localhost.jpg"><br>
      locahhost:3000으로 기본 포트가 3000번임을 확인 할 수 있습니다.<br>      
      <h4>■다음과 같은 에러가 뜨는 경우..</h4>
         <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/npm_cmd_error.jpg">   
         프로젝트 폴더(create-react-app를 이용해서 만든my-app)가 아닌 경우 다음과 같은 에러나 나타납니다. 현재 실행 폴더를 my-app으로 변경해서 실행합니다.   <hr/>      
1. # 프로젝트 완성 후 배포하기 위해 build하기
      프로젝트 폴더안의 VSCode terminal에서 npm run build 실행. 서버에 올리기위해 압축하는 과정   
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/npm_run_build.jpg"/>   
1. # serve 설치 및 실행   
      1. 서버 설치 : npm install serve -g   
      1. 서버 실행 : serve -s build   
      <img style="border:3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/serve_install_exe.jpg"/>     
      <h4> ■다음과 같은 에러가 뜨는 경우..</h4>   
         <img style="border: 3px solid black;border-radius:9px;width:800px;height:200px;" src="../../imgs/react/powershell_executionPolicy_error.jpg"/>   
         ps에서 직접 스크립트를 실행할 수 없도록 막아놓은 보안 정책 때문입니다.   
         <img style="border: 3px solid black;border-radius:9px;width:780px;height:400px" src="../../imgs/react/powershell_executionPolicy_change.jpg" />   
         get-executionpolicy로 현재 실행정책을 가져오면 restricted로 되어있는데 set-executionpolicy 실행 후 executionPolicy을 6가지 실행정책 중 가장 권장하는 RemoteSigned로 해주시면됩니다   
      1. 결과화면   
      <img style="border: 3px solid black;border-radius:9px;width:680px;" src="../../imgs/react/serve_complete.jpg" />   

