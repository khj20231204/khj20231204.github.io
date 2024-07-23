---
layout: single
title: 07_16.업캐스팅&다운캐스팅 사용예
categories: JAVA(Lesson)
tag: []
---

1. # 업캐스팅
   ```java
		
		/*
		자동 형변환(업 캐스팅)   
		1.자식 클래스에서 부모 클래스로 형변환을 하는 것   
		2.참조 가능한 영역이 축소된다.   
		3.컴파일에 의해 자동 형변환이 된다.
		*/
		
      //ex1.
		//Calendar c = new Calendar(); //Calendar클래스가 추상클래스기 때문에 기본생성자로 객체 생성 안됨
		Calendar c = Calendar.getInstance();
		
		Calendar c1 = new GregorianCalendar(); //업캐스팅, Calendar(부모 클래스) = GregorianCalendar(자식 클래스)
		GregorianCalendar c2 = new GregorianCalendar();
		
      //ex2.	
		//List는 인터페이스라 자체적으로 객체 생성을 할 수 없다.
		//List li = new List();				//에러발생
		List list = new ArrayList();		//업캐스팅
		ArrayList list2 = new ArrayList(); 
		
      //ex3.
		//add(Object e)
		list.add(10);		//Object e = new Integer(10);  	박싱 + 업캐스팅
		list.add(3.14);		//Object e = new Double(3.14);	박싱 + 업캐스팅
		list.add('j');		//Object e = new Character('j');박싱 + 업캐스팅
		list.add(true);		//Object e = new Boolean(true);	박싱 + 업캐스팅
		list.add("자바");		//Object e = new String("자바");	박싱 + 업캐스팅
		
		//boolean equals(Object an)
		
		//Object an = new String("java");		//업캐스팅
		if("java".equals(new String("java"))) {
			System.out.println("같은 값");
		}else {
			System.out.println("다른 값");
		}
		
		//Object an = new Integer(30);			//업캐스팅 + 박싱
		//Object an = 30;						//업캐스팅 + 자동 박싱
		if(new Integer(30).equals(new Integer(30))) {	//업캐스팅 + 박싱
			System.out.println("같은 값");
		}else {
			System.out.println("다른 값");
		}
		
		//Object an = new Double(3.14);			//업캐스팅 + 박싱
		//Object an = 3.14						//업캐스팅 + 자동 박싱
		if(new Double(3.14).equals(new Double(3.14))) {
			System.out.println("같은 값");
		}else {
			System.out.println("다른 값");
		}
   ```

1. # 다운 캐스팅
   ```java
      /*
		강제 형변환(다운 캐스팅)   
		1.부모 클래스에서 자식 클래스로 형변환   
		2.참조 가능한 영역이 확대   
		3.개발자가 직접 강제 형변환을 해야 함. 이때 강제 형변환시 자료형을 생략할 수 없음
		*/
		
         //ex1.
		List lt = new ArrayList();		//업캐스팅
		
		//add(Object e)
		lt.add(new String("자바"));		//업캐스팅
		lt.add("오라클");
		lt.add("JSP");
		lt.add("스프링");
		lt.add("파이썬");
		lt.add("텐스플로우");
		
		//Object get(int index)
		Object obj = lt.get(0);
		String s = (String)lt.get(0);		//다운 캐스팅(강제 형변환)
		
		for(int i=0 ; i<lt.size() ; i++) {
			String str = (String)lt.get(i);	//다운 캐스팅(강제 형변환)
			System.out.println(str);
		}
		
      //ex2.
		List ls = new ArrayList();		//업캐스팅
		
		//add(Object e)
		ls.add(10);					//업캐스팅 + 자동 박싱
		ls.add(200);
		ls.add(3000);
		ls.add(40000);
		ls.add(500000);
		
		//Objet get(int index)
		for(int i=0 ; i<ls.size() ; i++) {
			Object e = ls.get(i);
			
			Integer it = (Integer)ls.get(i);	//다운 캐스팅
			int n = it.intValue();				//언박싱
			
			int n2 = ((Integer)ls.get(i)).intValue(); //다운 캐스팅 + 언박싱
			System.out.println(n2);
		}
   ```