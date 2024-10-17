---
layout: single
title: 프로시저 사용
categories: MYSQL
tag: []
author_profile: false
---
 
1. # 기본 프로시저 사용

   while문 사용   

   ```sql
      CREATE DEFINER=`jspid`@`%` PROCEDURE `new_procedure`()
      BEGIN
         declare i INT DEFAULT 1;
         WHILE i < 100 DO

            SET i = i + 1;
         END WHILE;
         SELECT i;
      END
   ```

   호출 : call new_procedure();

   while문 안에서 insert into 실행하기   
   ```sql
      CREATE DEFINER=`jspid`@`%` PROCEDURE `new_procedure2`()
      BEGIN
         DECLARE I INT DEFAULT 1;
         WHILE I <= 100 DO
            SET I = I + 1;   
            INSERT INTO BOARD53(BOARD_NAME, BOARD_RE_REF) VALUES('AA',I);
         END WHILE;
      END
   ```
   호출 : call new_procedure2();