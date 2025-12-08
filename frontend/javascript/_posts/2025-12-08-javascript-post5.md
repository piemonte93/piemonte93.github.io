---
layout: post
related_posts:
  - /frontend/javascript/
title: "this & arrow function 연습문제"
date: 2025-12-08 20:41:04 +0900
image:
  path: "/assets/img/img-folder/js-img.jpg"
categories:
  - frontend
  - javascript
description: >
    'this & arrow function 연습문제 및 해설'
---
<br>

## <span style="color:#EBE1AB">1. 간단한 메소드 만들기</span><br>

<span style="color:#EBE1AB">사람</span>이라는 오브젝트가 하나 있다.<br>
이 오브젝트에 sayHi라는 함수를(메소드를) 하나 추가하고 싶다.<br>

```js
var 사람 = {
    name: '손흥민',
}

사람.sayHi(); // 안녕 나는 손흥민
```

<br>
위의 코드처럼 <span style="color:#EBE1AB">사람.sayHi()</span>이라고 작성하면 콘솔창에 <span style="color:#EBE1AB">안녕 나는 손흥민</span>이라는 글자가 나와야한다.<br>
'손흥민'이라고 이름을 하드코딩해서 출력하기보다는 실제 내 오브젝트에 있는 name에 해당하는 값이 출력되면 참 좋을것 같다.<br>
<span style="color:#EBE1AB">Q. sayHi()라는 함수를 어디서 어떻게 만들면 될까?</span><br>

<details>
<summary>답안</summary>
<div markdown="1">

```js
var 사람 = {
    name: '손흥민',
    sayHi: function() {
        console.log('안녕 나는 ' + this.name);
    }
}

사람.sayHi(); // 안녕 나는 손흥민
```

</div>
</details>

<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">2. 오브젝트 내의 데이터를 전부 더해주는 메소드 만들기</span><br>
<br>
오브젝트가 하나 있다.<br>

```js
var 자료 = {
    data : [1,2,3,4,5]
};
```
그런데 이 오브젝트에 <span style="color:#EBE1AB">전부더하기()</span>라는 함수를 하나 만들어서 사용하고 싶다.<br>
<br>
<br>
<br>

```js
var 자료 = {
    data : [1,2,3,4,5]
};
자료.전부더하기();
```

위처럼 자료.전부더하기()라고 쓰면 <span style="color:#EBE1AB">자료.data</span> 안에 있는 모든 숫자를 더해서 콘솔창에 출력해주어야 한다.<br>
(아마 15가 뜨겠지?)<br>
<span style="color:#EBE1AB">Q. 어떻게 코드를 짜면 될까?</span><br>
<span style="color:#EBE1AB">조건) 자료 object 줄괄호 내에 코드 작성 금지</span><br>
<br>
<details>
<summary>답안</summary>
<div markdown="1">

```js
var 자료 = {
    data : [1,2,3,4,5]
};

자료.전부더하기 = function() {
    var 합 = 0;
    this.data.forEach(function(a) {
        합 += a;
    });
    console.log(합);
}
자료.전부더하기();
```
</div>
<br>
</details>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">3. setTimeout 이용해보기</span><br>
<br>
자바스크립트엔 setTimeOut이라는 유용한 함수가 있다.<br>
특정 코드나 함수를 x초 후에 실행하고 싶을 때 사용하는 함수이다.<br>
어떻게 쓰냐면<br>

```js
setTimeout(콜백함수, ms단위의 시간)
``` 
<br>이렇게 쓰면 된다.<br>
<br>
<br>
<br>
예를 들어보면<br>

```js
setTimeout(function(){ console.log('안녕') }, 1000)
```
<br>이렇게 한줄 쓰면 1000ms(1초) 후에 왼쪽에 있는 콜백함수 내의 코드를 실행해 준다.<br>
그럼 1초후에 안녕이 콘솔창에 출력이 된다.<br>
<br>
또는 콜백함수자리에 직접 만든 함수를 넣을 수도 있다.<br>
역시 예를 들어보면<br>

```js
function 함수() {
    console.log('안녕');
}

setTimeout(함수, 1000)
```
<br>이렇게 콜백함수 대신 내가 미리 만들어놓은 함수의 이름을 적어도 실행된다.<br>
다만 콜백함수자리에 내가 만들어놓은 함수를 입력하고 싶으면 소괄호는 뺴야한다.<br>
setTimeout 개념정리 끝.<br>
<br>
<br>
<br>
<br>
<span style="color:#EBE1AB">본격 문제 들어간다.</span><br>
버튼을 클릭하면 지금 누른 버튼에 담긴 글자를 출력하는 기능을 만들고 싶어서 이렇게 코드를 짰다.<br>
<br>
<br>

```html
<button id="버튼">버튼이에요</button>

<script>
    document.getElementById('버튼').addEventListener('click', function(){
        console.log(this.innerHTML)
    });

</script>
```
<br>
그럼 콘솔창에 '버튼이에요'라는 글자가 출력되는가? 잘 된다.<br>
<br>
<span style="color:#EBE1AB">Q. 그럼 setTimeout을 이용해서 1초 후에 this.innerHTML을 콘솔창에 출력하고 싶으면 어떻게 코드를 수정해야 할까?</span><br>
1초 후에 '버튼이에요'라는 글자가 콘솔창에 등장하면 성공이다.<br>
<br>
<details>
<summary>답안</summary>
<div markdown="1">

```html
<button id="버튼">버튼이에요</button>

<script>
    document.getElementById('버튼').addEventListener('click', function() {
        setTimeout(() => { console.log(this.innerHTML) }, 1000);
    });

</script>
```
<br>
<br>
또는 옛날 스타일로 이렇게도 가능하다.<br>
<br>

```html
<button id="버튼">버튼이에요</button>

<script>
    document.getElementById('버튼').addEventListener('click', function() {
        var 버튼 = this;
        setTimeout(function(){ console.log(버튼.innerHTML) }, 1000);
    });

</script>
```
</div>
</details>