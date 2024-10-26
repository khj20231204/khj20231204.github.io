---
layout: single
title: Sql과 Java의 Date와 Timestamp
categories: SPRING
tag: []
author_profile: false
---

1. # date와 timestamp

   Sql도 데이터 타입으로 date와 timestamp가 있고, 
   Java도 데이터 타입으로 Date와 Timestamp가 있다

   Sql이 date이면 java도 date이고
   sql timestamp이고 java도 timestamp이면 서로 형변환이 필요없는데

   각자 데이터 타입이 다르면 형변환을 해야한다

   *java가 timestamp이고 sql이 date인 경우는 오류가 발생할 수 있기 때문에 사용하지 않음   

   Timestamp <->  Timestamp
   ```
      import java.sql.*;

      // ... (JDBC 드라이버 로딩, 연결 설정 등)

      PreparedStatement pstmt = conn.prepareStatement("SELECT timestamp_column FROM your_table");
      ResultSet rs = pstmt.executeQuery();

      if (rs.next()) {
         Timestamp timestamp = rs.getTimestamp("timestamp_column");
         // Timestamp 객체를 사용하여 원하는 작업 수행
      }
   ```

   Date <->  Date
   ```
      import java.sql.*;

      // ... (JDBC 드라이버 로딩, 연결 설정 등)

      PreparedStatement pstmt = conn.prepareStatement("SELECT date_column FROM your_table");
      ResultSet rs = pstmt.executeQuery();

      if (rs.next()) {
         Date date = rs.getDate("date_column");
         // Date 객체를 사용하여 원하는 작업 수행
      }
   ```

   java:Date <-> sql:Timestamp
   ```
      import java.sql.*;

      // ... (JDBC 드라이버 로딩, 연결 설정 등)

      PreparedStatement pstmt = conn.prepareStatement("SELECT timestamp_column FROM your_table");
      ResultSet rs = pstmt.executeQuery();

      if (rs.next()) {
         Timestamp timestamp = rs.getTimestamp("timestamp_column");
         Date date = new Date(timestamp.getTime());
         // Date 객체를 사용하여 원하는 작업 수행
      }
   ```

   java:Timestamp <-> sql:date => 오류가 발생할 수 있기 때문에 사용하지 않음