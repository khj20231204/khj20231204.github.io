---
layout: single
title: Service를 service와 servieImpl로 나누는 경우
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # Service를 Service와 ServiceImpl로 나누는 경우

   MVC패턴을 만든 이유가 각 기능 별로 컴포넌트화하여 각 클래스간 밀접성과 연결성을 약화하여 유지 보수를 편하게 하기 위해서 MVC 아키텍쳐를 선택했다. 마찬가지 이유로 연결성을 약화하기 위해서 선언부분(Service) 실행부분(Impl)을 따로 설계하는 것이 원칙으로 알고 있는데 지금 강사님의 소스를 보면 스프링에서는 분리를 했는데 스프링 부트에서는 분리를 하지 않았다. 프레젠테이션으로 강의를 하시는 부분과 본인이 만들었다곤 하는데 프로젝트별 변수 선언 방식, DTO 위치 등이 다 상이해서 강사님 실력에 믿음이 가지 않는다.   

   일단 새로운 부분이기 때문에 정리를 해놓는다.   

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