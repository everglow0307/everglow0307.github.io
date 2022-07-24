---
title:  "Array.prototype.slice.call(Arguments) 쓰임새"
excerpt: "Array.prototype.slice.call()과 arguments가 뭐야"

categories: 
  - react
tags:
  - [react]

toc: true
toc_sticky: true
 
date: 2022-07-24
---

리액트 공부하던 중 생소한 코드를 보게 되었다.

```javascript
function func() {
  var args = Array.prototype.slice.call(this, arguments);
  var first = args[0];
  var others = args.slice(1, args.length);
}

func(...args) { var [first, ...others] = args; }
```

Array.prototype.slice.call(this, arguments);
가 너무 낯설어서 관련 개념을 찾아보던 중, 몇 가지 알게 된 사실들을 정리한다.<br><br>


## :one: prototype이란?

자바스크립트는 프로토타입 기반 언어로, 함수를 사용해 객체를 생성할 때 원형이 되는 Prototype객체가 존재하며 새롭게 생성된 객체는 이를 참조한다.

Object,Function,Array 등 모두 함수로 정의되어 있으며, 함수가 생성될 때는 Prototype Object도 같이 생성된다.

function A() {} 라고 정의했을 때,
A라는 이름의 Prototype Object가 생기고
함수A에는 생성된 원형객체를 참조하는 prototype속성이 추가된다.

또한 추가적으로 함수 A를 이용해 var test = new A(); 로 test라는 객체를 만들면, A의 prototype 객체를 참조하는 __proto__ 라는 속성이 추가된다. 


![캡처](https://user-images.githubusercontent.com/71758210/180632889-44874bd9-695a-443f-aa10-8929c414fd3a.PNG)

따라서, 원형객체에 추가한 속성들은 이를 바라보는 객체들도 해당 속성을 사용할 수 있다.

```javascript
function A() {}

A.prototype.number = 3;
var test = new A();

console.log(test.number);  // 3이 출력
```
위와 같이 test라는 변수에 number속성을 추가하지 않았음에도 __proto__속성으로 상위 프로토타입 A객체와 연결되어  number값을 출력할 수 있는것이다. 이러한 형태를 프로토타입체인이라고 한다.

이러한 프로토타입체인에 의해 모든 객체의 부모인 Object Prototype 객체 내 모든 속성을 사용할 수 있는 것이다. 

<br>
## :two: call(), apply(), bind() 얘네는 뭘까

이해한 개념은 셋 다 함수의 prototype이 가지는 속성으로, this로 사용되는 객체를 명시적으로 지정해준다는 것이다.

this는 현재 함수를 부른 객체가 누구인지를 나타낸다.

A라는 객체안에서 this는 A를 명시하고, 전역에서 this는 window객체를 명시한다. 

this는 일반 함수에서 실행 / 객체 내부의 속성인 메소드에서 실행 / 생성자 실행 / 간접 실행 / Arrow Function등에 따라 실행문맥이 달라진다. 이는 다음에 정리해야 겠다.  
  

<details>
<summary>참고할 블로그</summary>
<div markdown="1">
[this 정리](https://kim-solshar.tistory.com/42)
[스코프와 클로저](https://kim-solshar.tistory.com/39)
</div>
</details>
<br>

> Func.call(thisArg[, arg1[, arg2[, ...]]])

첫번째 인자는 this의 실행문맥을 결정할 객체를 뜻하고,
두번째부터는 함수내에서 사용될 인수를 뜻한다.

```javascript
const A = {
  name: 'J'
};

const B = {
  name: 'S',
  say: function() {
    console.log(this.name+'가 말한다.');
  }
};

B.say();  // S가 말한다.

B.say.call(A); // J가 말한다.
```

정리하면, B라는 객체의 메소드인 say라는 함수 내 this가 바라볼 객체를 A로 지정하고, 마치 A내 속성인 것처럼 say함수를 호출하는 것이다.

<br>
## :heavy_check_mark:핵심

> Array.prototype.slice.call(this, arguments);

따라서, 처음에 낯설었던 위의 코드는 이렇게 이해할 수 있다.
<u color="red"><strong>array가 아닌 유사배열형태의 arguments를 Array객체 내 slice메소드를 호출해서 새로운 배열형태로 만드는 것이다.</strong></u>

이는 element.childNodes나 document.querySelectorAll과 같은 메서드에 의해 반환되는 NodeList와 같이 유사배열 형태의 객체를 배열형태로 만들 때 사용된다.


그러나 사실, 
<u color="red">Array.from과 전개 연산자</u>를 사용해 보다 간결하게 배열을 만들 수 있다.
  
    
      
> 참고

[prototype 정리](https://www.nextree.co.kr/p7323/)<br>
[call,apply,bind 정리](https://aljjabaegi.tistory.com/524)








