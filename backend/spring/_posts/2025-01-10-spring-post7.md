---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (7)"
image: 
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-10 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-10 수업 정리'
---

객체간의 의존성을 외부에서 주입하는 방식으로, 객체 간의 결합도를 낮추고 유연성과 재사용성을 높인다.
- 객체들의 의존성을 느슨하게 하는게 좋음.

외부에 서버가 있을경우 war, 일반적으론 jar

spring web , spring boot devTools, lombok 
- dependency로 추가
{이미지 추가}

JDBC -> JPA -> Spring Data JPA

Servlet(순수 자바 코드) -> JSP(HTML중심 + 자바 코드)

디자인을 바꾸려고 하는데 Controller랑 View가 강결합이 되어서 둘다 수정해야하는 문제가 생김. (Model1 방식)
-> 유지보수도 뒤지게 어려워짐

Model2 방식

Controller -> 비즈니스 로직에 집중

View는 -> 표현에 집중
{이미지}

Model, View, Controller로 분리해서 하기 때문에 MVC 방식이라고 한다.

Web server + Web Application Server
(정적인 리소스) (동적 리소스)

http -> Hyper Text Transfer Protocol
//127.0.0.1:8080/
에서 의미하는것들

//127.0.0.1 -> IP, 도메인
:8080 -> 포트번호 (Tomcat 기본 포트번호가 8080이다)
/   -> 루트경로

HTTP 요청방식
 - GET : URL에 쿼리스트림 방식으로 데이터를 담어서 요청
 - POST : HTTP 메시지 바디에 데이터를 담아서 요청
 - PATCH, PUT, POST....

localhost:8080/login?id=abc&pw=1234 -> GET방식

{이미지}
에러는 해당 부분을 보면 된다.
응답코드
- 404 : Not Found

general incoding utf-8