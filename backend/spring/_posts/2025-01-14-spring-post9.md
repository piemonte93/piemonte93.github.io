---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (9)"
image:
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-14 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-14 수업 정리'
---

/register 같은 절대경로 방식은 이클립스나 IntelliJ 같은 IDE에서는 될수도 있지만 배포했을 경우 안될 경우가 있기 때문에 /를 빼고 적어주는게 좋다.

HTML form 태그에서 서버에서는 id속성을 읽지 못한다. name과 value만 읽을 수 있다. 따라서 form 태그 내에 있는 html 요소들은 태그에 name과 value중 하나는 있어야 한다.

회원가입 형식은 get방식을 사용하지 않는게 일반적이다. url에 민감함 데이터들이 나타나서는 안되기 때문이다. 따라서 post 방식을 사용한다. post방식을 사용하려면 html form 태그에 method=post와 controller에 

@PostMapping을 사용하면 된다.

패키지를 만들때는 항상 com.example.web 내부에 만들어야 Spring에서 인식을 할 수 있다.

@ModelAttribute -> 클래스로 한번에 받는 방법

경로 변수
- @GetMapping(value)

회원정보 조회 (예시)
- http://localhost:8080/userInfo?user_id=1

REST API 방식으로 회원정보 조회
1. /users/1
- users는 변하지 않는 값이고 이후의 1부터 변할수 있으므로 이러한 것을 경로변수라고 한다.

개발자도구 application storage cookies에서 쿠키 목록을 볼 수 있다. 도메인 별로 저장이 된다. 쿠키는 나보다 상위 경로에 있는 것을 볼 수 없다. 쿠키는 다른사람이 봐도 알수가 없거나, 봐도 상관없는 것들을 저장해야 한다.

HttpServletResponse
- 응답객체

Thymeleaf에서 쿠키를 읽어오는 기능을 제공한다 @CookieValue

Thymeleaf 관련 문서를 보고 싶으면 thymeleaf.org 에서 참고하면 된다.

해당 HTML은 Thymeleaf를 적용하였다는걸 명시하는 법
- <html xmlns:th="http://www.thymeleaf.org"> 라고 html 태그에 적어주면 된다.

Controller는 클라이언트가 요청한 값을 처리해야 한다. Model이라는 객체 담아서 View에 전달하면 View에서 풀어서 Html을 렌더링해서 클라이언트한테 Response.

Model -> spring framework꺼를 import해야함

<span th:text="${data}">데이터</span> 에서 th 부분은 span의 속성이 아님. thymeleaf 문법이다.

Thymeleaf에서 문자열에 있는 html태그를 문자가 아닌 실제 html 태그로 반영하게 하려면 span th:utext나  

~~~html
  <li>${userA['name']} <span th:text="${userA['name']}"></span></li>
  <li>${userB.name} <span th:text="${userB.name}"></span></li>
  <li>${userB.getId()} <span th:text="${userB.getId()}"></span></li>
~~~

위 3가지 방식으로 표현이 가능하다.