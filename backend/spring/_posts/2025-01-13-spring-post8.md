---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (8)"
image:
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-13 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-13 수업 정리'
---

https://calico-zinc-99e.notion.site/SpringBoot-fd4ef190a04a4c75abfd70b4372111ec

정적인 페이지는 static에, 동적인 페이지는 templates에 보관

패키지는 최소한 com.example.java랑 같거나 하위로 해야 한다.

Spring에 들어오는 모든 요청은 일단 DispatcherSevelt에서 다 받는다.

요청의 내용을 보고 누가 처리해야하는지 분석을 하여 처리를 할수 있는 Controller를 찾는다. 처리 가능한 Controller가 있다면 전달.

스프링에서는 객체를 생성하는 일을 개발자가 직접 하지 않아도 된다. 필요하다면 개발자가 직접 관리 가능한 객체도 있다.

스프링 컨테이너에서 필요할떄 미리 만들어 넣어준다. -> 의존성 주입 (Dependency Injection)

스프링 빈

스프링 빈에 등록하는 방법은 2가지가 있다.

1. @Component라는 어노테이션 사용.

해당 어노테이션이 붙어있으면 스프링 빈이 자동으로 관리.

목적에 따라 @Service, @Repository, @Controller 어노테이션을 사용할 수 있다.

@Service

- 비즈니스 로직에 붙여줌

@Repository

- DB와 연동되는 클래스에 붙여줌

@Controller

- Controller 역할을 하는 클래스에 붙여줌

Component라는 방식에서 명시적인 기능이 들어간 것으로 보면 된다.

2. @Configuration 어노테이션을 클래스에 붙여주고 각 메서드마다 @Bean 어노테이션을 붙여주는 방식.

객체 생성에 대한 권한을 Spring에게 위임한 것으로 보면 된다. 제어의 역전이라고 하여 IoC라고 한다.

Spring에서 중요한 기능들

- DI(Dependency Injection)
- IoC
- AOP

@Component 등의 어노테이션이 붙어있으면 컴포넌트 스캔을 통해 서버가 시작할 때 스프링이 자동으로 객체로 생성.

개발자도구 네트워크 눌려보면 요청내용들이 나온다. Headers -> RequestMethod를 보면 어떤 방식으로 요청을 했는지 알수 있다.

@RequestMapping보다는 @GetMapping을 많이 사용한다

@ResponseBody

- return 그대로 출력되게 하는 어노테이션

HTTP 통신

1. Start Line

- URL, Method(GET, POST....) 정보가 들어간다.

2. Header

- 요청에 대한 메타(부가)정보

3. Message Body

- 실제 내가 보내는 데이터 영역. GET방식은 Body영역이 비어있다. POST 요청 시 Body에 담아서 보내준다.
  HTML 화면으로 담을수도 있다. 요청의 주체에 따라서 달라진다. 사람이 요청 할 경우 화면을 봐야하기 때문에 HTML로 응답을 하고, 기계가 요청할 경우(API 요청 등) 문자로 응답을 한다.

implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'

템플릿 엔진

스프링에서 HTML 렌더링을 위한 도구 (Thymeleaf, 머스태치 등)

SSR Server Side Rendering
CSR Client Side Rendering -> 리액트, 뷰

400번대 에러 -> 클라이언트가 요청을 잘못함
500번대 에러 -> 서버에서 처리 중 오류 발생

```java
package com.example.web.controller;

import jakarta.servlet.http.HttpServletRequest;
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@Slf4j
@RestController // 클래스 내 메소드의 리턴값을 메시지바디에 담아서 리턴한다.
public class RequestParamController {

    @GetMapping(value = "requestParamV1")
    public String requestParamV1(HttpServletRequest request) {
        String param = request.getParameter("param");
        String id = request.getParameter("id");
        log.info("param: {}", param);
        log.info("id: {}", id);

        return "ok";
    }

    @GetMapping(value = "requestParamV2") // 이 방식을 쓰면 String타입 말고 다른 타입도 받을 수 있다.
    public String requestParamV2(@RequestParam(name = "param") String param,
                                 @RequestParam(name = "id") String id) {
        log.info("param: {}", param);
        log.info("id: {}", id);

        return "ok";
    }
}
```

V1에서는 param이나 id나 둘중 하나가 없어도 에러가 발생하지 않고 null로 받아서 출력한다. 하지만 V2에서는 하나라도 빠지면 에러가 뜨면서 실행조차 안된다.
V2는 에러 탐지에 효율적임.

오늘의 과제
회원가입 하기
회원가입 폼을 HTML로 만들어서 회원가입 하기 버튼을 클릭하면 폼에 입력한 내용을 서버에서 읽어서 로그로 출력

회원가입 폼에 들어갈 내용

아이디, 패스워드, 이름, 성별(라디오), 이메일 주소(이메일은 텍스트, 도메인은 셀렉트로 처리)
버튼 누르면 서버에 요청됨
