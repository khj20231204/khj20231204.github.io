---
layout: single
title: (HTML)meta,pre,b와strong,첨자,버튼 비활성화,테이블
categories: CSS&HTML
tag: []
---



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

