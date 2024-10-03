---
layout: single
title: Styled Component와 CSS 적용
categories: REACT
tab: 
---

1. # React에서 스타일 적용하는 방법
   1)인라인 방식   
   : 태그 요소 안에 style을 입력 후 직접 스타일을 적용하는 방식입니다. 컴포넌트 내에서 직접 스타일을 지정하는 방식으로 간단한 스타일 변경에는 유용하지만, 스타일 관리가 어렵고 코드 가독성이 떨어질 수 있습니다. => style이후 {{}}(중괄호 2개)   

   2)CSS 모듈 방식   
   :: 컴포넌트별로 독립적인 CSS 파일을 만들고, CSS 클래스 이름이 전역적으로 충돌하지 않도록 하는 방식입니다. 스타일 엔캡슐레이션이 가능합니다.

   3)CSS 외부 파일   
   : 별도의 CSS 파일을 만들어 스타일을 정의하고, 클래스 이름을 이용하여 컴포넌트에 적용하는 방식입니다. 스타일 관리가 용이하고 재사용성이 높지만, 파일 관리가 필요합니다.   

   4)Styled Component   
   : CSS-in-JS 라이브러리입니다. 기존의 CSS 파일을 별도로 관리하는 방식에서 벗어나, 컴포넌트 내에서 JS 템플릿 문자열을 이용하여 직접 스타일을 정의할 수 있도록 해줍니다.

1. # CSS 적용 방식 예제
   요소 내부에 스타일을 직접 적용합니다.

   ```javascript
      import '../App.css'  //외부 모듈 경로
      .outer {
      background-color: pink;
      font-weight: 600;
      }

      //CSS 객체
      const inlineStyle = {
         color : 'white',
         backgroundColor : 'blue'
      }

      const StyleComponentEx = () => {

      //CSS 모듈
      
      return (
         <div style={{textAlign:'center'}}>
            
            //인라인 방식 {{ }},{}
            //직접 적용 : style=괄호 두개
            <div style={{color:'red',fontWeight:'bold',fontSize:'14px'}}>inline mode</div>
            //객체 적용 : style=괄호 한개
            <div style={inlineStyle}>CSS module</div>

            //CSS 외부 파일. App.css import
            <div className="outer">outer file</div>
         
         </div>
      );
   }
   ```

1. # Styled Component
   JS 템플릿 문자열로 스타일을 정의할 수 있습니다. 컴포넌트 개념이기 때문에 변수명의 가장 __앞 글자는 대문자__ 를 사용해야 합니다. 하나의 파일 안에서 스타일 지정과 코드를 함께 사용할 수 있으며 스타일의 재사용성도 높습니다.      

   설치하기
   ```
      npm install styled-components
   ```
   *component가 아니라 component__s__ 입니다.

   사용시 import를 해서 사용합니다.   
   ```javascript
      import styled from 'styled-components'  //import

      //하나의 컴포넌트를 생성(재사용)

      const StyledUL = styled.ul`  //ul이란 가상의 요소 생성, StyledUL - 앞 글자 대문자
         list-style-type: none
      `
      const StyledLi = styled.li`  //li란 가상의 요소 생성
         font-size: 15px;
         font-weight: bold;
      `
      const StyledDivOutLine = styled.div`  //div란 가상의 요소 생성
         border : 1px solid black;
         padding: 5px;
      `

      const Header = () => {
         return (
            <StyledDivOutLine>
               <StyledUL>
                  <StyledLi>메뉴 1</StyledLi>
                  <StyledLi>메뉴 2</StyledLi>
               </StyledUL>
            </StyledDivOutLine>
         );
      };

      //실제 html에 나타난 소스
      <div class="sc-gQaihK cTBnpn">
         <ul class="sc-eauhAA dTWtlT">
            <li class="sc-fFoeYl ca-dmfG">메뉴 1</li>
            <li class="sc-fFoeYl ca-dmfG">메뉴 2</li>
         </ul>
      </div>
   ```

1. # styled component의 삼항 연산자
   조건에 따라 다른 스타일 값을 적용할 수 있습니다.   

   ```javascript
      //부모 Homepage.js
      let [userName] = useState('saram');

      return(
         <>
         <Home userName={userName} />
         </>
      )

      //자식 Home.js
      const Home = (props) => {
         
         let {userName} = props;

         //StyledUserButton 앞에 S는 대문자!
         let StyledUserButton = styled.button`  
            color : ${userName === 'saram' ? 'blue' : 'red'}
         `
         return (
            <>
               <StyledUserButton>사용자 버튼</StyledUserButton>
            </>
         )
      }
   ```

1. # Link에 styled 적용시키기
   ```javascript
      import { Link } from 'react-router-dom';
      import styled from 'styled-components'

      //Link를 import후에 ( ) 안에 삽입
      let StyledLink = styled(Link)`
         color : red;
         padding: 20px;
         margin-top: 10px;
      `
   ```