---
layout: post
related_posts:
  - /frontend/javascript/
title: "Canvas API"
date: 2024-12-22 23:47:47 +0900
image: 
  path: https://blog.logrocket.com/wp-content/uploads/2021/05/javascript-svg-canvas.png
categories:
  - frontend
  - javascript
description: >
  'Canvas API를 이용하여 Javascript만으로 그림을 그릴수가 있다.'
---

JS에서 canvas를 사용해 브라우저에 2D 혹은 3D 그래픽을 그릴 수 있다.
html에서는 canvas 한 번 써주는 게 전부이고,나머지 작업은 대부분 js에서 이루어진다.

## 1. JS에서 canvas 불러오기
~~~js
const canvas = document.querySelector("canvas");
~~~
<br>

## 2. context 작성
context는 캔버스에 그림을 그릴 때 사용하는 붓이다.<br>
canvas.getContext 로 불러온 다음 2d를 선택한다. (주의! d 소문자임)
{:.note.smaller}
<br>

## 3. 캔버스 크기 설정
css에서 캔버스 크기 설정을 한 후 js에서도 작성해준다.
이후에는 width 와 height를 js에서만 수정할 것임 (css에서 X)
{:.note.smaller}
<br>

## 4. 캔버스 위에 사각형 그리기
### canvas 좌표 시스템
캔버스 좌상단이 좌표 0.0, 가로 X, 세로 Y
사각형 채우는 함수 fillRect 작성
{:.note.smaller}
~~~js
ctx.fillRect(x값, y값, w값, h값);
~~~
<br>

## 5. 캔버스 위에 원 그리기
~~~js
ctx.arc(x값, y값, 지름, 시작할 각도, 원이 끝날 각도);
/*
    ex)
    ctx.arc(250, 100, 50, 0, 2 * Math.PI);
*/
~~~

원이 시작하는 각도의 기준은 해당 그림을 참조하면 이해하기 쉽다.
![arc image](https://www.w3schools.com/tags/img_arc.gif)
{:.note.smaller}
출처 : https://www.w3schools.com/tags/canvas_arc.asp
<br>

## 기타정보
~~~js
CanvasRenderingContext2D.rect()
//너비와 높이로 결정되는 크기로 (x, y) 위치에 사각형의 경로를 만듭니다.

CanvasRenderingContext2D.fillStyle
// 도형 내부에 사용할 색상 또는 스타일. 기본 #000(검은색).

CanvasRenderingContext2D.beginPath()
// 하위 경로 목록을 비워 새 경로를 시작합니다. 새 경로를 만들려면 이 메서드를 호출하세요.
~~~

기타 정보 출처: https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D
<br>

~~~js
moveTo(x, y); // 브러쉬의 좌표를 움직여줌
lineTo(x, y); // 라인을 그려줌
~~~

수평인 직선을 그리려면 두 y값이 같아야 한다
라인이 끝난 점이 다음에 시작하는 브러쉬 좌표이다
정리하자면 fillRect = fill+Rect = fill + (moveTo+lineTo)
{:.note.smaller}
<br>

## (연습) 선으로 사각형 그리기

~~~js
ctx.moveTo(50, 50);
ctx.lineTo(100, 50);
ctx.lineTo(100, 100);
ctx.lineTo(50, 100);
ctx.lineTo(50, 50);
ctx.fill();
~~~