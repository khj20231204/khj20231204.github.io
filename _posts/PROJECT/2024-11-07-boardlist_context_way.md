---
layout: single
title: boardlist화면 해석
categories: PROJECT
tag: []
author_profile: false
---   

1. # boardlist부분 해석
   
   메인 -> 게시판 클릭 -> 클라이언트 : useEffet에서 axios 실행 -> 서버 : 스프링 Controller -> Board.jsx🎮   

  Board.jsx의 구성 컴포넌트   
  SearchForm : 검색 부분   
  BoardForm : 게시판 list 보여주는 부분   
  Pagenation : 페이징 부분   
   
   1️⃣useEffect에서 axios의 비동기 방식으로 Controller에 값 전달 후 받기   
   ```javascript
      - Board.jsx - 

      useEffect(() => {

        if(page === '' || page === null)
          page = 1;

        try{
        response = await boardapi.list(page, board);
          }catch(error){
          console.log(error);
        }

        setPage(response.data.currentPage);
        setTotalPage(response.data.pp.totalPage)
        setBoardList([...response.data.list]); //흩뿌리기
      })
   ``` 
   
   2️⃣컨트롤러에서 받은 결과값인 list를 map을 이용해서 BoardForm으로 출력   

   3️⃣Board DTO에 들어갈 search와 keyowrd 값과 현재 페이지 값은 컴포넌트 별로 사용 빈도가 높기 때문에 context로 만든다.   
   BoardContextProvider에서 선언한 변수와 함수를 다른 컴포넌트들 끼리 공유한다   

   - BoardContextProvider.jsx -   
   1-1)context선언   
   ```javascript
      export const BoardContext = createContext(); 선언   
   ``` 

   1-2)공유할 변수 선언   
   ```javascript

      //변수 선언
      let [page, setPage] = useState();
      let [search, setSearch] = useState();
      let [keyword, setKeyword] = useState();

      //변경 함수 선언
      const setPageFunc = (v) => {
         setPage(v)
      }

      const setSearchFunc = (v) => {
         setSearch(v);
      }

      const setKeywordFunc = (v) => {
         setKeyword(v);
      }
   ```

   1-3)변수를 props로 넘기면서 children을 감싸준다   
   ```javascript
      return (
         <div>
         <BoardContext.Provider value={{page, search, keyword, setPageFunc, setSearchFunc, setKeywordFunc}}>
            {children}
         </BoardContext.Provider>
      </div>
      );
   ```

   - Board.jsx에서 사용 - 
   1-1)import   
   ```javascript
      import { BoardContext } from '../contexts/BoardContextProvider';
   ```

   1-2)useContext선언
   ```javascript
      let {page, search, keyword, setPageFunc, setSearchFunc, setKeywordFunc} = useContext(BoardContext);
   ```


  