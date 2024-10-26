---
layout: single
title: 어노테이션
categories: SPRING(Lesson)
tag: []
author_profile: false
---
 
1. # @Controller
   @Controller 어노테이션은 Controller 기능을 수행 할 수 있도록 만들어 주는 역할을 합니다.   

   ```java
      @Controller
      public class HomeController {

         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(Locale locale, Model model) {
            Date date = new Date();
            DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
            String formattedDate = dateFormat.format(date);
            model.addAttribute("serverTime", formattedDate );
            return "home";
         }
      }
   ```

1. # @RequestMapping
   @RequestMapping 어노테이션은 클라이언트의 요청을 받을때 사용하는 어노테이션입니다.   

   ```java
      @Controller
      public class HomeController {

         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(Locale locale, Model model) {
            Date date = new Date();
            DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
            String formattedDate = dateFormat.format(date);
            model.addAttribute("serverTime", formattedDate );
            return "home";
         }
      }
   ```

1. # @RequestParam
   @RequestParam 어노테이션은 name 으로 값을 받을때 사용하는 어노테이션이다.   
   @RequestParam(“name”) 어노테이션은 request.getParameter(“name”)와 같은 역할을 한다   

   ```java
      @Controller
      public class HomeController {
         @RequestMapping(value = "/", method = RequestMethod.GET)
         public String home(@RequestParam(“name”) String name, Model model) {
         }
      }
   ```

1. # @ModelAttribute
   @ModelAttribute 어노테이션은 DTO클래스로 값을 받을때 사용하는 어노테이션이다.

   ```java
      @Controller
      public class HomeController {
         @RequestMapping(value = "/", method = RequestMethod.GET)
            public String home(@ModelAttribute BoardDTO board, Model model) {
         }
      }
   ```