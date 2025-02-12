---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (4)"
image: 
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-07 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-07 수업 정리'
---
[JPA 강의자료 노션][jpa-notion]

쿼리는 전부 alias를 붙여서 생성된다.

영속상태의 엔티티가 변경이 되면 자동으로 감지하여 update를 실시함.


@Entity 가 붙은 클래스는 JPA가 관리하는 엔티티이다.
main 메소드 실행할때 @Entity 어노테이션을 찾아서 전부 테이블로 만든다.

@Entity(name = "member") 같이 네임 속성을 줘서 변경이 가능하다.

enum (열거형)
- 열거형 타입은 대문자로 쓰는게 관례이다.
- 단순히 정해진 구분값들을 나열해서 적는다.
~~~ java
public enum Gender {
    MALE, FEMALE
}
~~~

primary key는 business logic과 관계없는 값으로 정하는것이 좋다.

primary key에 기본형 변수 말고 레퍼런스 변수를 쓰는 이유는, 기본형 변수는 초기화 하지 않으면 0이 들어가는데 이게 0을 넣은건지 아니면 초기화 안한건지 구분이 안되기 때문이다.
레퍼런스 변수는 초기화 하지 않으면 null이 들어가기 때문에 구분이 쉽다.

1. 테이블 전략
키 생성 전용 테이블을 만듬
~~~mysql
create table primary_key (
    key bigint
)
~~~
2. Auto Increment 전략
3. Sequence 전략
4. 수동 입력

MySQL에서는 @GeneratedValue(strategy = GenerationType.AUTO)는 비효율적이다.
MySQL에서는 @GeneratedValue(strategy = GenerationType.IDENTITY)를 쓰는게 좋다.

{이미지 추가}
한 책은 여러명에게 빌려질 수 있다.
한 멤버는 여러권을 빌릴 수 있다.
-> 클래스 관점

{이미지 추가}
관계형 DB 관점
1대 다의 관계

~~~java
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.List;

import jakarta.persistence.Entity;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.ManyToOne;
import jakarta.persistence.OneToMany;
import lombok.Data;

@Data
@Entity
public class Loan {
	@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	
	@ManyToOne // loan의 입장에서 다대일의 관계
	@JoinColumn(name = "member_id") // foreign key 설정
	private Member member;
	
	@ManyToOne // loan의 입장에서 다대일의 관계
	@JoinColumn(name = "book_id") // foreign key 설정
	private Book book;
	
	// book과 member에서는 loan을 알수가 없다. -> 단방향 연관관
	private LocalDate loanDate; // LocalDate: 시간을 알려주는 클래스
	private LocalDate returnDate;
	
	@Enumerated(value = EnumType.STRING)
	private LoanStatus status;
	
	@OneToMany(mappedBy = "member") // member의 입장에서 보면 일대다의 관계
	private List<Loan> loans = new ArrayList<>();
}

~~~
단방향 설정은 필수이고 양방향 설정은 선택이다.
양방향 설정을 할 경우 복잡해져서 안하는 것이 좋다.
[jpa-notion]: https://calico-zinc-99e.notion.site/JPA-16eb10cf26d88022907afb79746e0b7e
