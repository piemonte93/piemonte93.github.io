---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (1)"
image: 
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2024-12-30 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2024-12-30 수업 정리'
---

Group ID: 도메인의 역순 (com.naver)<br>
Artifact ID : 서비스 (프로젝트명)<br>
Maven 프로젝트 -> 외부라이브러리 자동으로 다운받고 관리할 수 있는 프로젝트<br>
<br>
자바 버전 변경하고싶은 경우(STS 기준)
프로젝트 우클릭 -> properties -> java build path -> Libraries -> JRE xx
<br>

~~~java
switch (option) {
                case 1 -> {
                    System.out.print("학생 이름을 입력하세요: ");
                    String name = scanner.nextLine();
                    System.out.print("학생 전공을 입력하세요: ");
                    String major = scanner.nextLine();
                    controller.addStudent(name, major);
                }
~~~
자바의 신문법으로써 switch문을 줄여서 쓰는 방법이다.
{:.note.smaller}

~~~java
case 1 : {
		System.out.print("학생 이름을 입력하세요: ");
                String name = scanner.nextLine();
                System.out.print("학생 전공을 입력하세요: ");
                String major = scanner.nextLine();
                controller.addStudent(name, major);
		break;
 }
~~~
위의 코드와 동일하다


사용자가 보는 화면 -> StudentManagementApp(UI) -> controller(Java, Spring) -> Repository(DB)


StudentManagementApp
StudentController
StudentRepositoryImpl 의존성 X

객체지향 설계의 5대 원칙(SOLOD)
1. SRP (Single Responsibility Principle): 단일책임 원칙
	- 하나의 클래스는 하나의 책임만 가져야 한다.
2. OCP(Open/Closed Principle) : 개방-폐쇄 원칙
	- 클래스, 모듈, 함수는 확장에 열려있고 수정에는 닫혀있어야한다.
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
	- 자식 클래스는 언제나 부모 클래스를 대체할 수 있어야한다.
4. ISP(Interface Segregation Principle): 인터페이스 분리 원칙
	- 클라이언트가 자신이 사용하지 않는 메서드에 의존하지 않도록 인터페이스를 분리해야 한다.
5. DIP(Dependency Inversion Principle): 의존관계 역전 원칙
	- 구체적인 구현 클래스가 아닌 추상화에 의존하도록 설계해야 한다.

파일로 저장하는 클래스를 추가로 만들었는데(확장), 원래 소스코드를 수정하는것은 좋은 코드가 아니다. (2번 원칙 위배)
-> 구현체가 아닌 추상화에 의존하도록 변경해두면 된다.(느슨하게 의존하도록 해야함)
