---
layout: single
title: fragments
categories: SPARTA2
tag: []
author_profile: false
---
 
1. # SPARTA2
    ```
        <div th:replace="~{fragments/sidebar :: sidebar}"></div>
    ```   
    th:replace : 해당 태그를 다른 템플릿 파일의 특정 부분으로 대체함.   
    ~{fragments/sidebar :: sidebar}   
    fragments/sidebar : templates/fragments/sidebar.html 파일을 의미함.   
    :: sidebar : sidebar.html 안에 있는 th:fragment="sidebar"을 가진 요소를 삽입함.   

    sidebar.html   
    ```
        <div th:fragment="sidebar">
            <ul>
                <li><a href="/home">Home</a></li>
                <li><a href="/profile">Profile</a></li>
                <li><a href="/settings">Settings</a></li>
            </ul>
        </div>

    ```

    main.html   
    ```
        <html xmlns:th="http://www.thymeleaf.org">
        <body>
            <header>Header 영역</header>
            <div th:replace="~{fragments/sidebar :: sidebar}"></div>
            <main>메인 콘텐츠</main>
        </body>
        </html>
    ```