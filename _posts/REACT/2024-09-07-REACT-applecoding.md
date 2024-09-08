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



