---
layout: single
title: 댓글과 검색 기능
categories: SPRING(Lesson)
tag: []
author_profile: false
---

1. # 댓글과 검색기능

1. # Sql 데이터
   ```
      create table board (
         num number primary key, -- primary key
         writer varchar2(20) not null, -- 작성자
         subject varchar2(50) not null, -- 제목
         content varchar2(500) not null, -- 내용
         email varchar2(30) , -- 이메일
         readcount number default 0, -- 조회수
         passwd varchar2(12) not null, -- 비밀번호
         ref number not null, -- 답변글끼리 그룹
         re_step number not null, -- 댓글 출력 순서
         re_level number not null, -- 댓글 레벨
         ip varchar2(20) not null, -- 작성자 ip
         reg_date date not null, -- 작성일
         del char(1) -- 글삭제유무(y or n) 
      );
   ```
   
원문 글과 댓글 글과 한테이블로 되어 있기 때문에 primary key를 sequeunce로 설정 못 합니다. ref값을 num값으로 가져와야 하는데 댓글을 입력해도 num값이 증가하기 때문입니다.   

1. # DTO
   ```
      @Data
      @Alias("board")
      public class Board {
         
         private int num;
         private String writer;
         private String subject;
         private String content;
         private String email;
         private int readcount;
         private String passwd;
         private int ref;
         private int re_step;
         private int re_level;
         private String ip;
         private Date reg_date;
         private String del;

         // page
         private int startRow;
         private int endRow;
         
         // 검색
         private String search;
         private String keyword;

      }
   ```
   page부분과 seacrh 부분이 추가 되었습니다.   
   mapper에 전달시 값이 되었든 주소가 하나의 값만 전달을 하기 때문에 map과 같은 collection에 데이터를 저장하거나 DTO에 필드를 추가해서 전할하게 됩니다. 지금은 DTO에 필드를 추가했습니다.   