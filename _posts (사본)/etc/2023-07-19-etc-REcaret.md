---
layout: single
title: 정규표현식
categories: etc
tag: [정규표현식]
---

1. # 기본 규칙
   대소문자를 구분합니다.  
   &nbsp;&nbsp;&nbsp; 소스 : Hello world   
   &nbsp;&nbsp;&nbsp; 표현식 : Hello   
   &nbsp;&nbsp;&nbsp; __Hello__ world : Hello가 검색됩니다.   
   &nbsp;&nbsp;&nbsp; 표현식 : hello   
   &nbsp;&nbsp;&nbsp; 결과 : Hello world : 일치하는 문자열이 없습니다.   
1. # 정규표현식에서 ^(서컴플렉스, 캐럿)사용   
   ^는 `[``]`(대괄호) 안에서의 사용과 밖에서의 사용 방식이 다릅니다.   
   ● 대괄호 밖에서 사용 : 문자열 시작을 의미   
   &nbsp;&nbsp;&nbsp; 소스 : who is who   
   &nbsp;&nbsp;&nbsp; 표현식 : ^who   
   &nbsp;&nbsp;&nbsp; 결과 : __who__ is who : 앞에 있는 who가 검색됩니다.    
   ● 대괄호 안에서 사용 : 부정, NOT을 의미합니다. 밑에서 다시 다룹니다.
   &nbsp;&nbsp;&nbsp; 소스 : who is who   
   &nbsp;&nbsp;&nbsp; 표현식 : [^who]   
   &nbsp;&nbsp;&nbsp; 결과 : who __is__ who : w,h,o 가 아닌 문자열만 선택되어 is가 검색됩니다.
1. # 정규표현식에서 $사용   
   문자열의 마지막에 위치하는 대상을 지정   
   &nbsp;&nbsp;&nbsp; 소스 : who is who   
   &nbsp;&nbsp;&nbsp; 표현식 : who$   
   &nbsp;&nbsp;&nbsp; 결과 : who is __who__ : 가장 마지막에 있는 who가  검색됩니다.   
1. # 특수문자에 `\`(escape) 사용   
   ^나 $와 같은 예약어를 검색하기 위해선 앞에 `\`를 붙입니다   
   &nbsp;&nbsp;&nbsp; 소스 : $12$`\`-`\`$25$   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : ^$   
   &nbsp;&nbsp;&nbsp; 결과 : $12$`\`-`\`$25$ : 검색되는 문자열이 없습니다.   
   &nbsp;&nbsp;&nbsp; 시작 위치의 문자를 검색하는 ^를 사용해서 첫 문자 $를 검색할 것 같지만 $가 예약어라 제대로 검색을 못 합니다.   
   &nbsp;&nbsp;&nbsp; 예약어는 앞에 `\`를 붙여서 예약어를 일반문자로 검색할 수 있습니다.   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `\`$   
   &nbsp;&nbsp;&nbsp; 결과 : __$__ 12 __$__ `\`-`\` __$__ 25 __$__   
   &nbsp;&nbsp;&nbsp; $를 일반문자로 취급해서 검색합니다.      
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : ^`\`$   
   &nbsp;&nbsp;&nbsp; 결과 : __$__ 12$`\`-`\`$25$ : 시작문자가 $인 것을 검색   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `\`$$   
   &nbsp;&nbsp;&nbsp; 결과 : $12$`\`-`\`$25 __$__ : "`\`$" 문자열을 의미하는 `\`$와 문장의 마지막을 의미하는 $    
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `\``\`   
   &nbsp;&nbsp;&nbsp; 결과 : $12$ __`\`__ - __`\`__  $25$ : 문자열 "`\`"를 검색   
1. # .(dot)의 사용
   .은 임의의 숫자, 문자, 특수문자 모든 것을 대신합니다.   
   &nbsp;&nbsp;&nbsp; 소스 : Hello 
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : ..   
   &nbsp;&nbsp;&nbsp; 결과 : __H__ __e__ __l__ __l__ o : 첫 두글자(H,e)가 검색, 뒤에 (l,l)이 검색되어 마지막 o만 남게됩니다.   
1. # .(dot) 검색하기   
   &nbsp;&nbsp;&nbsp; 소스 : O.K.   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `\`.   
   &nbsp;&nbsp;&nbsp; 결과 : O __.__ K __.__ : 임의의 문자 . 이 아니라 문자열 . 이 검색됩니다.   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `\`..`\`.   
   &nbsp;&nbsp;&nbsp; 결과 : O __.k.__ : "`\`." 문자열 . 뒤에 임의의 문자를 가리키는 예약어 . 이 있습니다.   
   &nbsp;&nbsp;&nbsp; 다시 그 뒤에 "`\`."문자열 . 이 되어 .K. 이 검색됩니다.   
1. # `[``]`사용 하기
   대괄호 안에 문자를 *하나씩* 매칭시켜 찾습니다.   
   &nbsp;&nbsp;&nbsp; 소스 : How do you do   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `[`you`]`   
   &nbsp;&nbsp;&nbsp; 결과 : H __o__ w d __o__ __y__ __o__ __u__ d __o__ : 대소문자 구분합니다.
1. # `[``]` 주의사항
   `[``]` 전체가 하나의 문자로 취급됩니다. [abc]. 가 나타내는 것은 a. or b. or c. 이 되어 `[``]`안에서 한 문자가 나오고 뒤에 . 이 딸려오는 방식입니다. "aababcefg" 문자열을 [abc]. 정규표현식으로 나타내면 a. , b. , c. 이 되어 (aa)(ba)(bc)가 선택되고 "efg"가 남게 됩니다.   
   &nbsp;&nbsp;&nbsp; 소스 : How do you do   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `[`dH`].`   
   &nbsp;&nbsp;&nbsp; 결과 : __Ho__ w __do__ you __do__ : d. , H. 이 검색됩니다.   
1. # -(대쉬)로 range범위 정하기
   `[`A-D`]`는 A,B,C,D와 같이 A~D까지 범위를 선택하게 됩니다. "ABCD" 문자열을 `[`A-C`]`로 나타내면 하나의 문자로 A,B,C 각각 검색을 하게되고 (ABC)가 선택되어 'D'만 남게 됩니다.
1. # `[``]`안에 ^ 사용하기
   ^이 `[``]`밖에서 사용되면 문자열의 시작을 의미하지만 `[``]`안에서 사용되면 부정,NOT을 의미하게 됩니다. `[`^ABC`]`는 `[``]`안에서 A, B, C가 각각 나오는데 A,B,C 이외의 문자열을 선택하게 됩니다.   
   &nbsp;&nbsp;&nbsp; 소스 : a3q7c8r9b2   
   <br>
   &nbsp;&nbsp;&nbsp; 표현식 : `[`^a-c`].`   
   &nbsp;&nbsp;&nbsp; 결과 : 3q78r92 : a,b,c를 제외한 문자열이 선택됩니다.