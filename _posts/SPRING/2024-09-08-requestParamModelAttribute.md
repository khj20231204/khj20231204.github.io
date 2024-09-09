---
layout: single
title: RequestRaram, ModelAttribute
categories: SPRING
tag: []
author_profile: false
---

1. # @RequestParam

   @RequestParam은 생략하면 기본적으로 적용되는 어노테이션입니다.   
   ```java
      @RequestMapping("/requestParam2")
      public String main1(String year){
            ...
      }

      //아래위 동일한 표현

      @RequestMapping("/requestParam2")
      public String main2(@RequestParam(name="year", required=false) String year){
            ...
      }
   ```   
   main1과 main2는 똑같은 코드입니다. main1에서 @RequestPara을 생략하면 main2와 같은 의미가 됩니다.    
   생략할 경우 required=false가 됩니다.   

   name='year'에서 year는 파라미터이름   
   required는 필수 여부입니다.   
   required=true : 필수   
   requried=false : 선택   

   주소창에 다음과 같이 입력할 경우   
   ```
      http://localhost/ch2/requestParam         //year=null, null출력
		http://localhost/ch2/requestParam?year=   //year="", 빈문자열 출력
		http://localhost/ch2/requestParam?year    //year="", 빈문자열 출력
   ```   

   ```java
      @RequestMapping("/requestParam3")
      public String main1(@RequestParam(name="year", required=true) String year) { 
         ...
      }

      //아래위 동일한 표현

		public String main2(@RequestParam String year) {   
         ...
      }
   ```   
   main1과 main2는 동일한 형식입니다. main2에서 @RequestParam을 명시해줬기 때문에 required=true가 됩니다.   

   주소창에 다음과 같이 입력할 경우   
    ```
      http://localhost/ch2/requestParam         //year=null, 404 error발생
		http://localhost/ch2/requestParam?year=   //year="", 빈문자열 출력
		http://localhost/ch2/requestParam?year    //year="", 빈문자열 출력
   ```   
   required=true인데 year=null이 입력된 첫번째 경우 400번대 error가 발생합니다.   

   ```java
      @RequestMapping("/requestParam5")
	   public String main3(@RequestParam(required=false, defaultValue="1") String year)
   ```   
   보통 required=false인 경우 defaultValue값을 설정합니다.   

1. # @ModelAttribute
   적용 대상을 Model의 속성으로 자동 추가해주는 어노테이션입니다. 반환 타입 또는 컨트롤러 메서드의 매개변에 적용 가능합니다.   

   ```java
      @RequestMapping("/getYoil")
      public String main(@ModelAttribute("myDate") MyDate date, Model m){
         ...
      }

      //아래위 동일한 표현

      @RequestMapping("/getYoil")
      public String main(@ModelAttribute MyDate date, Model m){
         ...
      }
   ```   
   값을 매개변수로 받으면서 바로 model에 저장합니다.   
   윗쪽의 @ModelAttribute("myDate") MyDate date는 date객체를 myData란 키값으로 저장하게 되고,   
   아랫쪽의 @ModelAttribute MyDate date에서는 __클래스 이름의 첫글자가 소문자__ 인 이름이 키값으로 저장됩니다.   

   __-반환 타입에 적용-__   
   반환 타입에도 ModelAttribute를 적용할 수 있습니다.   
   ```java
      private @ModelAttribute("yoil") char getYoil(MyDate date){
         return getYoil(date.getYear(), date.getMonth(), date.getDay());
      }
   ```   
   반환 타입으로 선언한 @ModelAttribute("yoil")부분에서 yoil이 키값이 되고 getYoil함수의 리턴 값이 value가 됩니다.    

   매개변수에 ModelAttribute는 생략가능합니다.   

   매개변수에 붙일 수 있는 어노테이션은 2종류가 있습니다.   
   RequestParam, ModelAttribute 2 종류가 있습니다.   

   타입이 참조형 - ModelAttribute 생략   
   기본형, String - RequestParam 생략   

   참조형일 때는 RequestParam을 붙일 수 없습니다.   
   기본형,String형은 param.으로 바로 접근이 가능하므로 model에 데이터를 저장할 필요가 없습니다.   

1. # ModelAttribute에 저장 과정
   public String main(@ModelAttribute MyDate date) 다음과 같이 MyDate란 클래스 형태가 Model에 저장되는 과정   

   ```java
      class MyDate{
         private int year;
         private int month;
         private int day;

         ...
      }

      public String main(@ModelAttribute MyDate date){
         ...
      }
   ```   
   MyDate란 클래스가 year, month, day를 멤버 변수로 가지고 있다고 가정한 경우   

   ```
      http://localhost/ch2/getYoil?year=2023&month=10&day=1
   ```   
   다음과 같은 주소로 요청이 일어난 경우   

   먼저 MyDate의 빈 객체가 만들어집니다.   

   MyDate    
   {0} --- year   
   {0} --- month   
   {0} --- day   

   이후 주소로 요청된 데이터들이 저장됩니다.   

   MyDate   
   {2021} --- year   
   {10} --- month   
   {1} --- day   

   이렇듯 빈 객체를 먼저 생성 후 요청된 값들이 빈 객체에 저장이 됩니다.   

   주소로 요청을 보낸 값들은 String이고 MyDate의 필드가 int인 경우 형변환이 이루어져야 합니다. 이것이 아래에서 말하는 WebDataBinder에 의해 처리됩니다.   

1. # WebDataBinder   

   WebDataBinder가 하는 일은 2가지 입니다.   
   1.타입 변환   
   2.데이터 검증   

   클라이언트의 데이터를 타입변환 후 유효성을 검증하게 됩니다. 이후 결과가 BindingResult로 넘어가고 이 값이 Controller에게 전달됩니다.   

   ```java
      @RequestMapping("/getYoil")
      public String main(@ModelAttribute MyDate myDate, BindingResult result){  //BindingResult호출
         ...
      }
   ```   
   BindingResult를 얻기 위해서는 바인딩할 객체의 바로 뒤에 선언되어야 합니다.   
   ```
      main(@ModelAttribute MyDate myDate, BindingResult result) 
   ```   
   다음과 같이 myDate객체의 바로 뒤에 BindingResult를 선언합니다.   



