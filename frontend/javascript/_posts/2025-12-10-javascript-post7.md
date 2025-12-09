---
layout: post
related_posts:
  - /frontend/javascript/
title: "변수 총정리 2. Hoisting, 전역변수, 참조"
date: 2025-12-10 04:33:53 +0900
image:
  path: "/assets/img/img-folder/js-img.jpg"
categories:
  - frontend
  - javascript
description: >
    '저번시간까진 선언, 할당, 범위라는 기초 필수 개념을 정리했는데<br>
    이번엔 변수의 부가 개념들을 정리해보도록 하자.'
---
<br>

## <span style="color:#EBE1AB">자바스크립트 변수, 함수의 Hoisting 현상</span><br>
<br>
자바스크립트는 변수나 함수를 선언하면 Hoisting이라는 현상이 일어난다.<br>
자바스크립트는 변수나 함수의 선언부분을 변수의 범위 맨 위로 강제로 끌고가서 가장 먼저 해석한다.<br>
그게 Hoisting 이다.<br>
<br>
<br>
<br>
예를 들어보자.

```js
function 함수() {

    console.log('hello');
    var 이름 = "Kim';

}
```
이렇게 함수 내에서 변수를 만들었다고 치자.<br>
근데 자바스크립트가 이 코드를 해석하는 순서는 이렇게 된다.<br>
<br>

```js
function 함수() {

    var 이름;
    console.log('hello');
    이름 = "Kim";

}
```

변수의 <span style="color:#EBE1AB">선언부분</span>을 강제로 변수의 범위 맨 위로 끌고가서 해석하고 지나간다.<br>
우리 눈에 보이진 않지만 자바스크립트는 코드 동작 순서가 이렇다.<br>
암튼 이게 Hoisting 현상이다.<br>
함수를 만들어도 똑같고, 변수를 let, const로 만들어도 똑같다.<br>
<br>
<br>
<br>
그럼 이 코드는 실행결과가 어떻게 될까?<br>

```html
<script>

    console.log(이름);
    var 이름 = 'Kim';
    console.log(이름);

</script>
```
<br>
<div style="background-color: #313436; padding: 30px;" >
<details>
<summary>뭘까요</summary>
콘솔창에 첫쨰로는 undefined가 출력되고<br>
둘째로는 Kim이 출력된다.<br>
왜냐면 Hoisting 때문에<br>
<div markdown = "1">

```js
var 이름;
console.log(이름);
이름 = 'Kim';
console.log(이름);
```
</div>
이런 순서로 코드가 실행되기때문이다.<br>
<br>
undefined라는건 변수가 선언은 되었는데 값을 아무것도 할당하지 않았을 때 undefined가 출력된다.<br>
일종의 자료형같은 것인데 그냥 <span style="color:#EBE1AB">정해지지않은 값</span>이라고 생각하면 된다.<br>
하지만 let,const 변수의 경우 Hoisting이 일어나긴 하는데 약간 이상한 방식으로 일어난다.<br>
그건 연습문제 강의에서 발견할 수 있다.
</details>
</div>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">변수 여러개 편리하게 만들기</span><br>
<br>
변수를 콤마로 구분하면 여러개를 동시에 만들 수 있다.<br>

```js
var 이름, 나이, 성별;
```
이렇게 하면 변수가 3개 생성된다. var 키워드 3번 쓰지않아도 되니 코드가 약간 더 줄어든다.<br>
<br>
<br>

```js
var 이름 = 'Kim', 나이, 성별;
```
선언과 동시에 할당도 하고 싶으면 그냥 이렇게 하면 된다.<br>
그냥 var let const 키워드를 여러번 안써도 된다는 장점이 있다.<br>
<br>
<br>

```js
var 이름,
    나이,
    성별;
```
어떤 놈들은 이렇게도 쓴다.<br>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">전역변수와 변수의 참조</span><br>
<br>
변수는 이런 특징이 있다.<br>
<span style="color:#EBE1AB">바깥에 있는 변수는 안쪽에서 자유롭게 사용가능</span>하다.<br>
이걸 전문 개발자용어로 참조가능하다 라고 한다만 자바스크립트에서는 이 현상을 부르는 다른 말이 있다.<br>
closure라고 한다.<br>
안쪽 바깥쪽이 뭔지 예를 들자면<br>
<br>

```js
var 나이 = 20;

function 함수() {
    console.log(나이);
}

함수();
```

지금 함수(){} 안쪽에서 바깥쪽에 있는 <span style="color:#EBE1AB">나이</span>라는 변수를 가져다 쓸 수 있다는 것이다.<br>
함수(){} 안쪽에 <span style="color:#EBE1AB">나이</span>라는 변수 정의가 있으면 그걸 쓰겠지만<br>
없으면 자연스럽게 바깥에 있는 변수를 가져다 쓴다.(참조한다)<br>
<br>
<br>
<br>
프로그래밍에선 <span style="color:#EBE1AB">전역변수</span>라는게 있다.<br>
모든 함수나 if나 for 내부에서 공통적으로 사용할 수 있는 (참조할 수 있는) 유용한 변수를 뜻한다.<br>
전역변수를 만들어 쓰고싶으면 그냥 script태그 열고 다짜고짜 변수 하나 만들면 된다.<br>
<br>

```html
<script>
    var 나이 = 20;

    function 함수() {
        console.log(나이)
    }
</script>
```
그럼 밑에 나오는 모든 함수, for, if 등에서 전부 나이라는 변수를 사용가능하다.<br>
전역변수 완성!<br>
근데 전역변수는 이상한 특징이 있다.<br>
<br>
<br>
<br>
예전에 window라는 오브젝트가 있다고 배웠다.<br>
window는 자바스크립트 기본함수 보관하는 큰 오브젝트라고 배웠다.<br>
alert, getElementById, console.log 이런 함수들이 다 들어있다.<br>
<br>
진짠지 테스트 해보려면<br>
자바스크립트 기본 함수들을 오브젝트 다룰 때 처럼 window.alert(), window.document.getElementById() 이렇게 사용해봐라.<br>
alert 이런것도 window에 보관된 애들이기 때문에 window.alert('안녕')이렇게 해도 잘 된다.<br>
이게 window 오브젝트의 역할이다. 끝!<br>
<br>
<br>
<br>
근데 <span style="color:#EBE1AB">쌩으로 전역변수를 만들면 window에도 보관</span>이 된다.(let 말고 var 키워드만)<br>
왜 그런지 궁금하면 역시 자바스크립트 만든 사람한테 물어보길 바란다<br>

```html
<script>
    var 나이 = 20;

    console.log(나이);
    console.log(window.나이);
</script>
```

나이라는 전역변수를 만들면<br>
<span style="color:#EBE1AB">자동으로 window 오브젝트에 보관</span>이 되었으니깐<br>
신기하게 window.나이를 써도 출력이 됩니다.<br>
(전역함수도 마찬가지로 window에 자동으로 보관된다)<br>
<br>
<br>
그래서 전역변수를 조금 더 엄격하게 관리하거나 구분짓고 싶으면<br>
전역변수를 만들 때와 사용할 때 window를 활용해보아라.<br>
<br>
```html
<script>
    window.나이 = 20; // 전역변수 만들기
    console.log(window.나이); // 전역변수 사용하기
    window.나이 = 30; // 전역변수 변경하기
</script>
```
이런식으로 사용할 수도 있다.<br>
프로그래밍 엄격히하는걸 좋아하는 변태들이 많이 이용한다.<br>
(node.js 환경에선 window 대체품인 global 이라는 오브젝트가 있다)<br>
<br>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">간단한 연습문제</span><br>
<br>
다음 코드를 실행하면 콘솔창에 무엇이 뜰까?<br>

```html
<script>
    
    if (true) {
        let a = 1;
        var b = 2;
        if (true) {
            let b = 3;
        }
        console.log(b);
    }

</script>
```
<br>
<div style="background-color: #313436; padding: 30px;">
<details>
<summary>답 펼쳐보기 전에 잘 생각해보도록 하자. 함정이 있을 수 있음</summary>
실은 함정없음<br>
b는 2라는 값이 출력된다.<br>
let b = 3; 이 부분은 안쪽 if 내에서만 존재하는 놈이니 바깥의 console.log(b)와는 무관하다.
</details>
</div>