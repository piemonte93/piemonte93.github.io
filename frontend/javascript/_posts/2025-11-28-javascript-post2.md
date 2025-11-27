---
layout: post
related_posts:
  - /frontend/javascript/
title: "this 키워드를 알아보자 1. 함수와 Object에서 사용하면?"
date: 2025-11-28 05:11:47 +0900
image:
  path: "/assets/img/img-folder/js-img.jpg"
categories:
  - frontend
  - javascript
description: >
  '개발하면서 은근 자주 찾아볼 수 있는 this 키워드는 뜻이 매우 다양하다. 사용하는 환경에 따라서 4개 이상의 각각 다른 뜻을 가지고 있는데  이번 기회에 총정리해보자.'
---

<br>
## 1-1. 그냥 쓰거나 함수 안에서 쓰면 this는 window를 뜻한다.

그냥 HTML 파일 아무거나 하나 만들고 중간에 `<script>`태그 열어서 일단 this라는 키워드를 콘솔창에 출력해보자.

```js
console.log(this);
```

그러면 this 키워드는 그냥 window {어쩌구} 이런 값이 나온다.

비슷하게 일반 함수 내에서 this라는 값을 불러보면

```js
function 간지나는함수() {
  console.log(this);
}
간지나는함수();
```

똑같이 this라는 값은 window라고 출력된다.
이것이 this의 첫째 뜻이다. 그냥 window다.

<span style="color:#EBE1AB">Q. window가 뭔가요?</span>
<br>
<span style="color:#EBE1AB">A. window는 모든 전역변수, 함수, DOM을 보관하고 관리하는 전역객체입니다.</span>
<br>

라고 구글검색 번역투로 설명하면 솔직히 이해가 안되니 좀 쉽게 비유해보자면 우리가 쓰는 자바스크립트 함수 document.getElementById(), alert(), console.log()
이런 함수들을 보관하는 보관소이다. 보관소는 특별한건 아니고 그냥 큰(오브젝트)일 뿐이다.

또한 전역변수를 만들었을 때도 이 값을 보관해준다.

```html
<script>
  var x = 300;
</script>
```

이렇게 변수를 큰 공간에 만들면 x라는 변수는 window라는 큰 오브젝트 안에 자동적으로 생성된다. 함수도 마찬가지이다.
아무튼 그냥 보관소이다. 끝!

<span style="color:#EBE1AB">*전역변수 : 코드 내 모든 곳에서 참조해서 쓸 수 있는 범용적인, 범위가 넓은 변수입니다. 그냥 script태그 내에 쌩으로 var 변수 하나 만들면 그건 자연스레 전역변수가 됩니다. </span>
<br>

## 1-2. strict mode일 때 함수 안에서 쓰면 this는 undefined 이다.

```html
<script>
  "use strict";

  function 간지나는함수() {
    console.log(this);
  }
  간지나는함수();
</script>
```

IE 10버전 이상에선 'use strict'라는 키워드를 페이지 최상단에 추가하면 strict mode로 자바스크립트를 작성가능하다.
strict mode에선 var 키워드 없이 변수를 선언하거나,
변수를 arguments라는 이상한 키워드로 선언하거나 그런 실수를 방지해준다.
strict mode에선 this 키워드를 일반함수 안에서 불렀을 때 undefined라는 값으로 강제로 지정해준다.

## 2. object 자료형 내에 함수들이 있을 수 있는데 거기서 this값은 '주인님'을 뜻한다.

object 자료형에 함수같은거 집어넣을 수 있단걸 아는가?

```js
var 오브젝트1 = {
  data: "Kim",
  간지함수: function () {
    console.log("간지");
  },
};
```

글자나 숫자 집어넣듯이 오브젝트 내에도 저렇게 함수를 집어넣을 수 있다.
그럼 함수를 어떻게 꺼내쓰냐면

```js
var 오브젝트1 = {
  data: "Kim",
  간지함수: function () {
    console.log("간지");
  },
};

오브젝트1.간지함수();
```

이렇게 쓰면 된다. 그럼 콘솔창에 '간지'라는 글자가 출력된다.
오브젝트에 들어가는 함수들을 있어보이는 전문용어로 메소드 method라고 칭한다.

근데 메소드 안에서 this를 쓰면 신기한 값이 나온다. 바로 주인님이라는 값인데

```js
var 오브젝트1 = {
  data: "Kim",
  간지함수: function () {
    console.log(this);
  },
};

오브젝트1.간지함수();
```

간지라는 단어 대신 this라는 키워드를 출력시키면 어떻게 되나?
콘솔창에 {data : 'Kim', 간지함수 : f} 뭐 이런 값이 출력되지 않나?
이게 뭐냐면 그냥 방금 만든 오브젝트1이다.
그래서 메소드안에서 this를 쓰면 <span style="color:#EBE1AB">this는 메소드를 가지고 있는 오브젝트</span>를 뜻한다.
쉽게 외우고 싶으면 this는 '메소드의 주인님'을 지칭한다.
