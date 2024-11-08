---
layout: single
title: DAO를 Dao와 DaoImpl로 나누는 경우
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # DAO를 Dao와 DaoImpl로 나누는 경우

   "Service를 Service와 ServiceImpl로 나누는 경우"에서 적었듯이 강사님 실력이 의심되긴 하지만 일단 정리를 해놓는다.   

   interface로 만든 Dao에서 선언만 하고, class로 만든 DaoImpl에서 실제 함수를 호출   

   ```java
      -Dao.java-

      public interface DeptDao {
         List<Dept> list();

         int insert(Dept dept);

         Dept select(int deptno);

         int update(Dept dept);

         int delete(int deptno);
      }
   ```

   DaoImpl에서 Respository를 선언하고 SqlSeesion을 이용해서 CRUD적용
   ```java
      -DaoImpl.java-

      @Repository
      public class DeptDaoImpl implements DeptDao {
         @Autowired
         private SqlSessionTemplate st;

         public List<Dept> list() {
            return st.selectList("deptns.list");
         }

         public int insert(Dept dept) {
            return st.insert("deptns.insert", dept);
         }

         public Dept select(int deptno) {
            return st.selectOne("deptns.select", deptno);
         }

         public int update(Dept dept) {
            return st.update("deptns.update", dept);
         }

         public int delete(int deptno) {
            return st.delete("deptns.delete", deptno);
         }
      }
   ```

1. # DAO를 Dao와 DaoImpl을 하나로 합친 경우

   주로 스프링 부트에서 이렇게 사용하는 듯...   

   @Mapper 어노테이션으로 의존성을 주입 하면 이후 바로 mapper.xml에서 실행   
   ```java
      -Dao.java-

      @Mapper
      public interface BoardDao {
         
         List<Board> list(Board board);
         int getTotal(Board board);
         int insert(Board board);
         Board select(int num);
         void selectUpdate(int num);
         int update(Board board);
         int delete(int num);
         int getMaxNum();
         void updateRe(Board board);
         
      }
   ```
