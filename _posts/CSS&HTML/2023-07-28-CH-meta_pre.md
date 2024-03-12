---
layout: single
title: (HTML)meta,pre,b와strong,첨자,버튼 비활성화,테이블
categories: CSS&HTML
tag: []
---

1. # meta
   1. ## 추가 정보 meta
      meta 태그를 입력하면 웹 페이지에서 부가적으로 나타내는 정보를 담을 수 있습니다.   

   1. ## 검색 엔진 키워드 등록
   ```html
      <meta name="keyword" content="파이썬,자바,머신러닝">   
   ```
   name속성에 keyword를 입력하면 content에 있는 내용을 검색 엔진이 찾아 웹 사이트에 노출시킵니다.   

   1. ## 인코딩 설정
   ```html
      <meta charset="utf-8">
   ```
   해당 웹 사이트를 utf-8형식으로 인코딩 합니다.   

   1. ##  검색된 경우 추가 설명 노출
   ```html
      <meta name="description" content="추가적인 설명 기록">
   ```
   브라우저가 해당 사이트를 검색한 경우 검색된 사이트가 어떤 사이트인지 추가 설명을 표시해줍니다.   

   1. ## 모바일 지원
   ```html
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```
   모바일에서도 접근할 수 있도록 반응형 웹을 사용하기 위해 viewport를 사용하여 선언   

1. # pre
   탭과 줄바꿈이 브라우저에 그대로 노출      

1. # b, strong   
   `<b>`와 `<strong>`모두 텍스트를 굵게 표시하는데, 검색 엔진은 strong을 특별히 강조

1. # 첨자
   1. ## 윗 첨자 sup   
   ```html
      a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup>
   ```   
   결과: a<sup>2</sup> + b<sup>2</sup> = c<sup>2</sup>   

   1. ## 아랫 첨자 sub   
   ```html
      C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>
   ```   
   결과: C<sub>6</sub>H<sub>12</sub>O<sub>6</sub>

1. # button
   1. ## 버튼 비활성화 : disabled   
   ```html
      <button disabled>버튼 비활성화</button>
   ```   
   결과: <button disabled>버튼 비활성화</button>   

1. # table
   1. ## 기본 테이블 모양
      <table border=2>
         <tr>
            <td>1</td>
            <td>2</td>
         </tr>
         <tr>
            <td>3</td>
            <td>4</td>
         </tr>
      </table>
   1. ## colspan : 가로 병합
   ```html
      <table border=2>
         <tr>
            <td colspan=2>1</td>
         </tr>
         <tr>
            <td>3</td>
            <td>4</td>
         </tr>
      </table>
   ```
   <table border=2>
      <tr>
         <td colspan=2>1</td>
      </tr>
      <tr>
         <td>3</td>
         <td>4</td>
      </tr>
   </table>
   1. ## rowspan : 세로 병합   
   ```html
      <table border=2>
         <tr>
            <td rowspan=2>1</td>
            <td>2</td>
         </tr>
         <tr>
            <td>4</td>
         </tr>
      </table>
   ```
   <table border=2>
      <tr>
         <td rowspan=2>1</td>
         <td>2</td>
      </tr>
      <tr>
         <td>4</td>
      </tr>
   </table>

