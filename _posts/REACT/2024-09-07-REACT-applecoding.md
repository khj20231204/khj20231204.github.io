---
layout: single
title: appleCoding
categories: REACT
tab: 
---

1. # JSX문법
  1.class(X) className{x}
  2.return문 안에서 {변수}는 상상하는 어디든 다 대입할 수 있다.   
  3.스타일을 넣을 때 이중괄호 사용
  4.뺄샘기호는 진짜 뺄샘으로 인식하기 때문에 '-' 생략 후 사용한다.   
    ```cs 
      <input style={{color:'red',fontSize:'16px'}}>
    ```   

  destructuring 
    ```cs
      let [a,b] = [1,2];
      
      //a=1, b=2가 할당
    ```   

  useState를 사용하면 html은 자동 재렌더링이 됨.   
  배열로 초기화 가능   
    ```cs
      let [글제목, setTitle] = useState(['남자 코트 추천','강남 우동 맛집','파이썬 독학'])
    ```   

    ```
      /* eslint-disable */
    ```   
  Warning 문 없애기   

  onClick={}안에 함수이름 넣기   
    ```
      <h4>{글제목[0]} <span onClick={() => {
            따봉변경(따봉 + 1)
          }}>👍</span> {따봉} </h4>
    ```

1. # 소스 정리
  ```javascript
   return (
      <div className="App">
         <h4 className="blogTitle"> React Blog</h4>
            <div>
               {subject.map((e, i) => { //e는 subject안에 값, i는 0부터 1씩 증가하는 정수
                  return(
                  <div key={i}>
                     <h4 className="list" onClick={() => {
                     //modal ? <Modal/> : null;
                     //modal ? setModal(false) : setModal(true);
                     setModal(true)
                     setNum(i);
                     }}>{e}<span onClick={(e) => {
                        /*
                        상위요소로 이벤트가 퍼지지 않는다. 이벤트 버블링을 막는다.
                        클릭을 하면 span태그, h4태그, div태그까지 3번의 클릭을 한 셈이 된다.
                        이벤트가 하위요소에서 상위요소로 퍼지기 때문에 하위요소에서 e.stopPropagation()을 사용한다. 
                        */
                        e.stopPropagation(); 

                        let copy = [...favorite]
                        copy[i] = copy[i]+1;
                        setFavorite(copy)
                     }}>👍</span>({favorite[i]})</h4>
                     <h5>{date[i]}</h5>
                     <button onClick={() => {
                        let delSubject2 = [...subject];
                        delSubject2.splice(i,1)
                        setSubject(delSubject2)
                     }}>글 삭제</button>
                     <hr/>
                  </div>
                  )
               })}
            </div>
                
            <button type="button" onClick={() => {
              let copy = [...subject]        //배열 값 변경
              copy[0] = '가을 여자 옷 추천'
              setSubject(copy.sort());
            }}>타이틀 변경</button> 
            <br></br>
            <input type="text" onChange={(e)=>{
               setTextValue(e.target.value); //useState의 set함수는 비동기처리됨
               console.log(textValue); //최초 한글자 입력은 출력되지 않음. set함수가 비동기처리되어서 
            }} ></input>

            <button onClick={() => {
               const newItem = textValue;
               setSubject([...subject, newItem]); //useState 배열 값 추가

            }}>글 제목 작성</button>

            <br></br>

            <button onClick={() => {
               let delSubject = [...subject];
               delSubject.splice(subject.length-1,1); //useState 배열 값 삭제
               setSubject(delSubject);
            }}>글 삭제</button>

            {/* 동적인 UI만드는 step
            1.html css로 미리 디자완성하기   
            2.UI의 현재 상태를 state로 저장   
            3.state에 따라 UI가 어떻게 보일지 작성 */}
            
            {/*
            if문 대신 삼항연산자
            {
               조건식 ? 참일 때 실행 : 거짓일 때 실행
            }
            */}

            {/*
            map함수
            array.map(function(e){})
            배열뒤에는 map을 사용가능
            1.array자료 갯수만큼 함수안의 코드 실행해줌 
            2.함수의 파라미터는 array안에 있던 자료
            3.return에 뭐 적으면 array로 담아줌
            */}

            {
               /* 모달에 값 넘기기 */
               modal ? <Modal colorV={color[num]} subjectV={subject} setSubjectV={setSubject} titleV={subject[num]}></Modal> : null
            }
      </div>
      )
    }

    /*컴포넌트 만드는 법
    1.function 만들고(다른 함수 밖에서 만든다)
    2.return()안에 html담기
    3.<함수명></함수명>쓰기
    */

    const Modal = (props) => {
      return(
          <div className="modal" style={{background:props.colorV}}>
            {/* {console.log(props)} */}
            <h4>{props.titleV}</h4>
            <p>날짜</p>
            <p>상세내용</p>
            <button onClick={() => {
                const copy = [...props.subjectV]
                copy[0] = '남자 코트 추천'
                props.setSubjectV(copy);
            }}>글 수정</button>
          </div>
      )
    }
    export default Blog;
  ```
