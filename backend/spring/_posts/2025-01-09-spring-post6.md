---
layout: post
related_posts:
  - /backend/spring/
title: "Springboot DSA 수업 정리 - (6)"
image: 
  path: ../../../assets/img/img-folder/springboot-img.jpg
date: 2025-01-09 12:40:40 +0900
categories:
  - backend
  - spring
description: >
  '2025-01-09 수업 정리'
---

@ManyToOne (fetch = FetchType.EAGER) -> 즉시 로딩
즉시로딩은 N+1 문제를 야기할 수 있다.
@ManyToOne (fetch = FetchType.LAZY) -> 지연 로딩

양방향은 디폴트가 지연로딩이다.
현업에서는 즉시로딩은 안쓴다고 생각