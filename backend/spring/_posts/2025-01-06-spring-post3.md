---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (3)"
image: 
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-06 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-06 수업 정리'
---

[JPA 강의자료 노션][jpa-notion]

# 엔티티
- 자바에서 다루는 객체와 DB에서 다루는 객체.

# Maven Repository에 getter와 setter 메서드와 toString 메서드를 쉽게 만들어주는 라이브러리
- lombok

pom.xml에 추가
~~~xml
<dependencies>
    원하는 라이브러리 추가
</dependencies>
~~~
dependencies 안에 원하는 라이브러리들을 추가해줘야 한다.

lombok annotation
- @Getter
- @Setter
- @ToString
- @EqualsAndHashCode
- @NoArgsConstructor
- @RequiredArgsConstructor
- @AllArgsConstructor

@Data는 모든 어노테이션을 포함하는 거지만 안쓰는 편이 좋다.

~~~java
		String str1 = "Hello";
		String str2 = "Hello";
		// new를 안쓰고 리터럴 값을 넣으면 같은 해쉬코드를 가르킨다.
		System.out.println(str1 == str2);
		String str3 = new String("Hello");
		String str4 = new String("Hello");
		// 새로 생성한것이므로 서로 다른것
		System.out.println(str3 == str4);
		System.out.println(str3.equals(str4));
~~~

~~~mysql
-- 라이브러리 데이터베이스 생성
create database libraries;

-- 계정 생성
create user 'library'@'%' identified by '1234';

-- 권한 부여
grant all privileges on libraries.* to 'library'@'%';

-- 권한 새로고침
flush privileges;
~~~

java resources 밑에 META-INF 폴더 생성

EntityManagerFactory emf = Persistance.createEntityManagerFactory("<persistence-unit name:""> 에 있는 name부분을 여기에 넣는다");

은행계좌 프로그램
- 입금 :
    잔고 += 입금액
- 출금 :
    잔고 -= 출금액
- 이체 (A출금 B입금 둘다 성공해야 commit)
1. A계좌 (1000) -> 출금(1000 -> 500)
2. B계좌 (2000) -> 입금(2000 -> 2000)

JPA에서 INSERT를 실행할땐 persist()를 사용한다.

~~~java
		// 영속성 컨텍스트에 저장
		System.out.println("book persist 전");
		em.persist(book1); // DM작업시작
		System.out.println("book persist 후");
~~~

위의 코드를 추가해서 실행해보면 다음과 같은 결과가 나온다.
{이미지 추가}
persist 전에 전,후가 전부 출력되는데 이는 persist는 영속성 컨텍스트에 저장하는 작업이기 때문이다. Insert를 실행한것이 아니다.

~~~java
		// 조회
		Book findBook = em.find(Book.class, 1L); // param1은 타입, param2는 primary key의 값이 들어간다. 여기서는 id값이 들어간다.
		System.out.println("findBook: " + findBook);
~~~
해당 조회문을 실행해보면 다음과 같은 결과가 나온다.
{이미지 추가}
Insert 이전에 조회가 되는것을 확인할 수 있는데, 이는 영속성 컨텍스트에서 1차 캐시에 저장하고 여기서 조회하는 것이기 때문이다.
{이미지 추가}

[jpa-notion]: https://calico-zinc-99e.notion.site/JPA-16eb10cf26d88022907afb79746e0b7e
