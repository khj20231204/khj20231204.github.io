---
layout: single
title: 페이징과 댓글
categories: SPRING(Lesson)
tag: []
author_profile: false
---

1. # 전체 소스
   ```java
      -Controller.java-

      //기본-1) 현재 페이지 번호   
      int page = 1;   
      //기본-2) 한 페이지에 출력할 데이터 갯수   
		int limit = 10; 
		
		if(request.getParameter("page") != null) {
			page = Integer.parseInt(request.getParameter("page"));
		}
		System.out.println("BoardListAction page:"+page);
		
		//기본-3) 총 데이터 갯수
		BoardDAO board = BoardDAO.getInstance();
		int listcount = board.getCount();
		
      //----- DB데이터 출력 값 -------

      //파생-1) 
		int startRow = (page-1) * limit + 1;
      //파생-2)
		int endRow = page * limit;	
		
		//게시판 목록 10개 구하기(startRow, endRow)
		List<BoardDTO> boardlist = board.getList(startRow, endRow);
		System.out.println("boardlist:"+boardlist);
		
      //----- 페이지네이션 -------

      //파생-3)
		int startPage = ((page-1)/limit)*limit + 1;
      //파생-4)
		int endPage = startPage + limit - 1; 
      //파생-5)
		int pageCount = listcount/limit + ((listcount % limit == 0) ? 0 : 1);
      
		if(endPage > pageCount) {
			endPage = pageCount;
		}
		
		//공유 설정
		//request객체로 공유해서 id는 세션, 나머지는 request => dispahter로 포워딩
		//int형은 ${page}로 el로 바로 출력 가능
		//list, array형은  foreach문에서 items에 먼저 삽입. request로 공유한 경우 
		request.setAttribute("page", page);
		request.setAttribute("limit", limit);
		request.setAttribute("listcount", listcount);
		request.setAttribute("boardlist", boardlist);
		request.setAttribute("pageCount", pageCount);
		request.setAttribute("startPage", startPage);
		request.setAttribute("endPage", endPage);
		
		ActionForward forward = new ActionForward();
		forward.setRedirect(false);
		forward.setPath("./board/board_list.jsp");
		
		return forward;
   ```

   ```jsp
      -list.jsp-

      <%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
      <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
      <%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
         
      <!DOCTYPE html>
      <html>
      <head>
      <meta charset="UTF-8">
      <title>게시판 목록</title>
      </head>
      <body>
         <a href="boardform.do">글작성</a><br>
         글갯수 : ${listcount } 개
         <table border=1 align="center" width="800">
            <caption><h3>게시판 목록</h3></caption>
            <tr>
               <th>번호</th>
               <th>제목</th>
               <th>작성자</th>
               <th>날짜</th>
               <th>조회수</th>
            </tr>
            
            <!-- 화면 출력 번호 -->
            <c:set var="num" value="${listcount-(page-1)*10 }"/>
            <c:forEach var="b" items="${boardlist }">
            <tr>
               <td>${num}
                  <c:set var="num" value="${num-1}"/>
               </td>		
               <td>
                  <a href="boardcontent.do?no=${b.no}&page=${page}">			
                     ${b.subject}
                  </a>
               </td>		
               <td>${b.writer}</td>		
               <td>
                  <fmt:formatDate value="${b.register}" 
                     pattern="yyyy-MM-dd HH:mm:ss"/>
               </td>		
               <td>${b.readcount}</td>		
            </tr>
            </c:forEach>		
         </table>

         <!-- 페이지 처리 -->	
         <center>
         <c:if test="${listcount > 0 }">

         <!-- 1page로 이동 -->
         <a href="boardlist.do?page=1" style="text-decoration:none"> < </a>	

         <!-- 이전 블럭으로 이동 -->
         <c:if test="${startPage > 10 }">
            <a href="boardlist.do?page=${startPage-10}">[이전]</a>
         </c:if>

         <!-- 각 블럭에 10개의 페이지 출력 -->
         <c:forEach var="i" begin="${startPage}" end="${endPage}">
            <c:if test="${i == page}">		<!-- 현재 페이지 -->
               [${i}]
            </c:if>
            <c:if test="${i != page}">		<!-- 현재 페이지가 아닌 경우 -->
               <a href="boardlist.do?page=${i}">[${i}]</a>
            </c:if>
         </c:forEach>

         <!-- 다음 블럭으로 이동 -->
         <c:if test="${endPage < pageCount }">
            <a href="boardlist.do?page=${startPage+10}">[다음]</a>
         </c:if>

         <!-- 마지막 페이지로 이동 -->
         <a href="boardlist.do?page=${pageCount}" style="text-decoration:none"> > </a>

         </c:if>
         </center>	
      </body>
      </html>
   ```
1. # pagenation
   페이지를 구성하기 위해서 기본적으로 가져오는 데이터가 3개 있습니다. 그리고 기본 데이터에서 파생되는 데이터가 5가지가 있는데, startRow, endRow는 DB의 데이터를 가져오는 값이 되고, startPage, endPage, pageCount는 하단의 페이지 목록을 구하는 데이터가 됩니다.   
   
   __-기본 데이터-__   

   기본-1)page : 현재 페이지로 클라언트의 선택으로 가져오는 페이지 번호입니다. 클라이언트로 넘어오는 값이으면 
   기본 1로 설정합니다.   
   << [1] [2] [3] [4] [5] [6] [7] [8] [9] [10] [다음] >> 중 택1   

   기본-2)limit : 한 페이지에 출력할 데이터 갯수입니다. limit에 따라 [1] [2] ... [11] 전체 페이지의 갯수가 달라집니다.   

   기본-3)listcount : 총 데이터 갯수로 db에 저장되어 있는 데이터 수가 됩니다.

   __-DB 데이터 출력 값-__   

   파생-1)startRow : 데이터베이스에서 가져올 가상의 rownum의 첫번째 수
   파생-2)endRow : 데이터베이스에서 가져올 가상의 rownum의 마지막 수

   (1)startRow, (2)endRow   
   => __데이터베이스의 데이터 rownum 수, 실제 board_num이 아니라 가상의 rownum__   
   
   startRow와 endRow는 page와 limit로 정의

   limit : 10   
   page=1 : startRow=1, endRow=10    
   page=2 : startRow=11, endRow=20   
   page=3 : startRow=21, endRow=30   

   limit : 5   
   page=1 : startRow=1, endRow=5   
   page=2 : startRow=6, endRow=10   
   page=3 : startRow=11, endRow=15   
   
   __-Pagenation 데이터-__   

   (3)startPage, (4)endPage, (5)pageCount
   ```js
		int startPage = ((page-1)/limit)*limit + 1; 
		int endPage = startPage + limit - 1;
      int pageCount = listcount/limit + ((listcount % limit == 0) ? 0 : 1);
   ```
   페이지 목록은 다음과 같은 형태를 가지고 있습니다.
   ```js
     << [1] [2] [3] [4] [5] [6] [7] [8] [9] [10] [다음] >> 
   ```  
   limit가 10이면 한 페이지 목록 당 1~10, 11~20, 21~30, ... 이처럼 정해진 크기만큼 for문을 돌면서 출력하게 됩니다.   
   이때 1,11,21 이 startPage가 되고,   
   10,20,30 이 endPage가 됩니다.   
   
   page:1   
   startPage : 1 , endPage : 10   
   page:4    
   startPage : 1, endPage : 10   
   page:10   
   startPage : 1, endPage : 10   
   <br>
   page:11   
   startPage : 11, endPage : 20   
   page:19   
   startPage : 11, endPage : 20   
   <br>
   즉,   
   page 1~10 => startPage: 1, endPage: 10   
   page 11~20 => startPage: 11, endPage: 20   

   (5)pageCount 총페이지 수
   160/10 + ((170%10 == 0) ? 0 : 1) = 16+0 = 16; 
   166/10 + ((170%10 == 0) ? 0 : 1) = 16+1 = 17;
   int형 끼리 연산 결과는 int형

   for문으로 무조건 startPage부터 endPage까지 출력할 경우   
   << [이전] [11] [12] [13] [14] [15] [16] [17] [18] [19] [20] [다음] >>   
   중 17페이지까지는 데이터가 있지만 18,19,20 페이지는 데이터가 없는 경우   
   마지막 총 페이지를 구해서 endPage에 입력하여 이를 방지하게 됩니다.   
   
   ```java
      if(endPage > pageCount) {
			endPage = pageCount;
		}
   ```   
   endPage : for문에 사용되어 무조건 출력되는 마지막 페이지   
   pageCount : 데이터가 있는 실제 마지막 페이지   
   
1. # 글목록 10개 쿼리문
   
   ```sql
      select * from (select rownum rnum, board.* from (select * from [테이블명] order by num desc) board) where rnum >= "startRow변수" and rnum <= "endRow변수";
   ```
   
   -쿼리문 해석-   

   ```sql
      Select * from (select rownum rnum, board.* from (내부쿼리1) board) where rnum >= "startRow변수" and rnum <= "endRow변수";
   ```
   내부쿼리1의 별명을 board로 두고 board.*는 내부쿼리1의 결과를 모두 다 가져온다

   내부쿼리1 : 전체를 내림차순정렬 - 최신 게시글을 가장 앞에 놓기 위해서 135번, 134번, 133번, 132번,… 이렇게 가장 마지막에 입력된 데이터를 가장 먼저 노출

   Select rownum rnum :  rownum은 db가 제공하는 가상의 순위 데이터, 내부쿼리1에서 내림차순정렬한 것을 순위를 매긴다. 