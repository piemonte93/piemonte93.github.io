---
layout: post
related_posts:
  - /fullstack/typescript/
title: "Javascript를 이용하지 않고 Typescript를 이용하는 이유"
date: 2024-12-25 00:26:47 +0900
image: 
  path: ../../../assets/img/img-folder/ts-image.png
categories:
  - fullstack
  - typescript
description: >
  'Javascript를 이용하지 않고 Typescript를 이용하는 이유는 안정성에 있다고 생각한다.'
---

<br>

Javascript를 안쓰고 Typescript를 쓰는 이유는 안정성, 더 정확히 말하면 타입 안정성에 있다고 생각한다. 이로 인해 얻을 수 있는 이점들이 있다.

## 코드에 버그 발생률이 줄어듬
<br>

![Javascript image](../../../assets/img/img-folder/js-img.jpg)

<br><br>
Javascript는 매우 유연한 언어이다. 아무리 멍청한 코드를 작성해도 개발자를 이해하려 하고 도와주려고 한다. 오히려 자바스크립트는 에러를 안 보여주려고 많은 노력을 한다. 그러나 이러한 유연성은 코드의 안정성을 떨어뜨리고 버그를 발생시키는 주범이다.

~~~js
[1, 2, 3, 4] + false;// '1, 2, 3, 4false'
~~~

‘1, 2, 3, 4false’ 라는 결과가 나오는데, 숫자 배열에 boolean을 더하는 연산을 하여 말도 안되는 연산결과를 에러없이 보여준다. 이는 다른언어에서는 허용하지 않는다.

~~~js
function divide(a, b) {
	return a / b;
}
divide(“xxxxxx”); // NaN
~~~
위의 함수를 정의했다면 해당 함수는 숫자가 파라미터로 들어올때만 연산이 되어야한다.<br>문제는 자바스크립트가 해당 함수를 올바르게 사용하는걸 강제하지 않는다는 것이다. 결국 divide(“xxxxxx”)은 NaN이라는 결과를 띄우고 에러없이 전혀 문제없이 돌아가게 된다. 입력값이 1개인데 실행되는 것도 문제이고 숫자가 아닌 값이 들어갔는데도 실행이 되는것도 문제이다.<br>
우리가 자바스크립트에게 a와 b가 숫자라는 것도 알려주지 않았기에 자바스크립트가 마음대로 추측해서 제한을 걸 수 없기 때문이다. 그냥 코드를 실행할 뿐이다.
~~~js
const piemonte = {name: piemonte”};
piemonte.hello();
~~~
위 코드를 실행하면 실행중에 에러가 나오는 런타임 에러가 발생하는데, 일반적인 언어들에서는 해당 객체에 hello()라는 함수가 없기에 실행전에 에러를 띄워준다.

## Typescript는?

**Typescript는 Strongly Typed Language(강타입 언어)이다. <br> 일반적인 컴파일러 언어들은 컴파일 시 어셈블리 코드나 바이트 코드가 되지만, Typescript는 컴파일 하면 Javascript 파일이 생성된다. Web은 Typescript를 이해할 수 없고 Javascript로 이해할 수 있기 때문이다. Node.js는 TS, JS 양쪽 모두 이해할 수 있다.**
{:.message}

<br>
Typescript는 변수 생성시 변수의 타입을 명시할 수 있다.

~~~ts
let a: number = 1;
~~~
위 코드는 변수 a를 생성할때 타입을 number로 명시해줘야 한다. 만약 다른 타입의 값을 넣으려 한다면 에러를 띄운다.
~~~ts
let a: number = 1;
a = “hello”; // 에러
~~~

Typescript는 데이터와 변수의 타입을 명시적으로 정의할 수도 있고 아니면 Javascript처럼 변수만 생성하고 넘어가도 된다. 후자의 방식으로 할 경우 Typescript는 타입을 대입값에 맞추어 추론한다.
~~~ts
let a = 1 // 변수만 생성. 대입된 1의 값을 통해 typescript에서 타입을 int로 추론함
let b : string = “abcd” // 변수의 타입을 명시적으로 정의
let c : number[] = [] // 숫자가 들어가는 배열인것을 명시
c.push(1)
~~~
가능한 Typescript가 추론하도록 명시하지 않는편이 편하다.{:.message}

추가적인 Typescript 문법은 나중에 더 올릴 예정이다.