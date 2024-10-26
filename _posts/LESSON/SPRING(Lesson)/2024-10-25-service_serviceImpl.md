---
layout: single
title: Service를 service와 servieImpl로 나누는 경우
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # Service를 Service와 ServiceImpl로 나누는 경우

   주로 스프링에서 이렇게 사용 하는 듯...   

   interface로 만든 Service에서는 선언만 하고, class로 만든 ServiceImpl에서 실제 함수를 호출   

   ```java
      -Service.java-

      public interface DeptService {
         List<Dept> list();

         Dept select(int deptno);

         int update(Dept dept);

         int delete(int deptno);

      }
   ```

   class로 만든 ServiceImpl에서 @Service 어노테이션과 @Autowired를 주입
   ```java
      -ServiceImpl.java-

      @Service
      public class DeptServiceImpl implements DeptService {
         @Autowired
         private DeptDao dd;

         public List<Dept> list() {
            return dd.list();
         }

         public Dept select(int deptno) {
            return dd.select(deptno);
         }

         public int update(Dept dept) {
            return dd.update(dept);
         }

         public int delete(int deptno) {
            return dd.delete(deptno);
         }
      }

   ```

1. # Service를 만들지 않고 ServieImpl만 사용하는 경우

   기능은 Service와 ServiceImpl을 나눴을 때와 같지만 Service를 사용하지 않고 ServiceImpl만 사용했다.   

   이런 경우 의존도와 결합도가 올라가서 컴포넌트화 해야하는 MVC의 기본 아키텍쳐에 위배가 되는데 왜 이렇게 하지..

   ```java
      -ServiceImpl.java-

      @Service
      public class BoardServiceImpl {
         @Autowired
         private BoardDao bd;
         
         public List<Board> list(Board board) {
            return bd.list(board);
         }
         
         public int getTotal(Board board) {
            return bd.getTotal(board);
         }
         
         public int insert(Board board) {
            return bd.insert(board);
         }
         
         public Board select(int num) {
            return bd.select(num);
         }
         
         public void selectUpdate(int num) {
            bd.selectUpdate(num);
         }
         
         public int update(Board board) {
            return bd.update(board);
         }
         
         public int delete(int num) {
            return bd.delete(num);
         }
         
         public int getMaxNum() {
            return bd.getMaxNum();
         }
         
         public void updateRe(Board board) {
            bd.updateRe(board);
         }
      }
   ```