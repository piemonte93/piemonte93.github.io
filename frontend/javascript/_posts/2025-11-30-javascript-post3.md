---
layout: post
related_posts:
  - /frontend/javascript/
title: "this 키워드를 알아보자 2. event listener와 constructor"
date: 2025-11-30 03:33:47 +0900
image:
  path: "/assets/img/img-folder/js-img.jpg"
categories:
  - frontend
  - javascript
description: >
  '저번 시간 this 의미 정리를 하자면
  1. 그냥 일반 함수에서 쓰면 window
  2. 오브젝트 내의 함수(메소드)에서 쓰면 함수를 동작시키는 오브젝트가 출력된다고 배웠다. 이번엔 다른 this 키워드의 의미들을 알아보자'
---
<br>

## <span style="color:#EBE1AB">3. constructor 안에서 쓰면 constructor로 새로생성 되는 오브젝트를 뜻한다.</span>

자바스크립트에서 오브젝트를 비슷한걸 여러개 만들고 싶을 경우 오브젝트를 복사하는게 아니라 constructor라는걸 만들어서 사용한다. 쉽게 말하면 constructor는 오브젝트 복사해서 생성해주는 기계이다. 기계를 어떻게 만드는지 알아보자.

```js
function 기계() {
    this.이름 = 'Kim';
}
```

이게 기계 만드는 법이다.<br>
함수 문법을 이용해서 만든 후, 안에 this. 어쩌구를 추가해주면 된다.<br>
여기서의 this는 <span style="color:#EBE1AB">기계로부터 새로 생성될 오브젝트</span>들을 의미한다.<br>


그럼 this.이름 = 'Kim' 이건 무슨 뜻일까?<br>
새로 생성되는 오브젝트의 이름 key값에 'Kim'이라는 value를 집어넣어줘!<br>
라는 뜻 아닐까?<br>
맞다.
<br>
<br>

▼이건 참고로 알아두면 좋은 기계에서 오브젝트 뽑는 법이다.

```js
function 기계() {
    this.이름 = 'Kim'
}
var 오브젝트 = new 기계();
```

이렇게 new 키워드를 이용하면 새로운 오브젝트를 꺼낼 수 있다.<br>
그리고 새로운 오브젝트는 {이름 : 'Kim'}이라는 값을 가지고 있다.<br>
(this 라는 키워드 덕분에)

<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">4. eventlistener 안에서 쓰면 this는 e.currentTarget 이라는 의미이다.</span>

이벤트리스너라는 문법 기억하는가?

```js
document.getElementById('버튼').addEventListener('click', function(e) {
    console.log(this)
});
```

여기서 this를 소환하면 이것은 바로 e.currentTarget이라는 뜻과 똑같은 의미이다.<br>
<span style="color:#EBE1AB">e.currentTarget은 지금 이벤트가 동작하는 곳</span>을 뜻한다.<br>
매우 간단히 설명하면 지금 addEventListener 부착된 HTML 요소를 뜻한다고 보면 된다.<br>
의심되면 ## <span style="color:#EBE1AB">e.currentTarget, this, document.getElementById('버튼')</span> 이거 세개를 각각 출력해보면 된다.<br>
이게 this의 마지막 뜻이다.
<br>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">case1. 이벤트리스너 안에서 콜백함수를 쓴다면 this는?</span>

이런 코드를 쓴다거 가정해보자.
<br>

```js
document.getElementById('버튼').addEventListener('click', function(e) {
    var 어레이 = [1,2,3];
    어레이.forEach(function(){
        console.log(this)
    });
});
```

이벤트리스너 안에서 forEach() 라는 반복문을 사용했다.<br>
forEach() 반복문을 사용할 땐 안에 function(){} 콜백함수를 집어넣어서 사용하게 되어있다. 그래서 넣었다.<br>
<span style="color:#EBE1AB">(* 콜백함수는 그냥 함수 안에 파리미터역할로 들어가는 함수를 뜻한다. 그게 다임)</span><br>
하지만 솔직히 forEach가 무슨 역할을 하는지는 몰라도 이건 알수 있다.

<br>
<span style="color:#EBE1AB">Q. 위의 코드에서 this를 출력하면 무엇이 나올까?</span>
> <details>
>    <summary>뭐가 나오냐면</summary>
>    <br>
>    바로 답보지말고 한참동안 생각을 해보도록 하자.<br>
>    생각이 안나면 지금까지 this의 1,2,3,4번 뜻을 각각 대입해 봐라.<br>
>    그럼 뭘까.<br>
>    <br>
>    4번뜻에 의하면..eventlistener 안에서 쓴건 아니다.<br>
>    eventlistener 내부는 맞지만 그 안에서 function을 하나 더 만났기 때문에 의미가 변한다.<br>
>    3번 뜻에 의하면.. constructor는 아닌거 같다.<br>
>    실은 this의 1번이나 2번 뜻이 맞다.<br>
>    저렇게 쌩으로 있는 콜백함수는 그냥 일반함수랑 똑같기 때문에 window가 출력된다.<br>
>    <br>
>    <br>
>    this의 값은 this가 어떤 함수안에 들어있는지만 잘 체크하면 바로 알 수 있다.
> </details>
<br>
<br>
<br>
<br>
<br>

## <span style="color:#EBE1AB">case2. 오브젝트 안에서 콜백함수를 쓴다면 this는?</span>
<br>
이번엔 이런 코드를 쓴다고 가정해보자
<br>

```js
var 오브젝트 = {
    이름들 : ['김', '이', '박'];
    함수 : function(){
        오브젝트.이름들.forEach(function(){
            console.log(this)
        });
    }
}
```

오브젝트라는 오브젝트 안에 이름들, 함수라는 자료를 각각 저장했다.<br>
함수라는 자료 안에 forEach 반복문을 돌렸는데,
<br>

<span style="color:#EBE1AB">Q. 그럼 여기 안에서의 this값을 출력하면 뭐가 나올까?</span>
> <details>
> <summary>뭐가 나오냐면</summary>
> 역시 잘 대입을 해보면 된다.<br>
> this값을 판단할 땐 가장 가까이 있는 함수를 살펴보면 된다.<br>
> <br>
> forEach()안에 있는 함수에 this가 들어있다.<br>
> 근데 이 함수는 무슨 뭐 특별한 역할을 하는 함수인가?<br>
> 아니다. 그냥 일반 함수일 뿐이다.<br>
> 그래서 이것도 window이다.
> <br>
> </details>

<br>
그래서 this값을 function을 만날 때마다 바뀔 수 있기 때문에 내가 원하는 this를 쓰기 힘든 경우가 있다. 그럴 땐 함수를 arrow function으로 바꿔보자.
<br>

```js
var 오브젝트 = {
    이름들 : ['김', '이', '박'];
    함수 : function(){
        오브젝트.이름들.forEach(() => {
            console.log(this)
        });
    }
}
```

자바스크립트 ES6 문법 중,<br>
function(){} 대신 쓸 수 있는 () => {} 이라는 arrow function 문법이 있다.<br>
똑같이 함수 만드는 문법이다.<br>
이걸 쓰면 함수 내부의 this 값을 새로 바꿔주지 않기 때문에 this를 사용할 때 유용하다.<br>
심심하면 사용하길 바란다. (아니면 애초에 this 키워드를 쓰지말자)<br>
자세한 arrow function에 관한 내용은 다음에 설명하겠다.