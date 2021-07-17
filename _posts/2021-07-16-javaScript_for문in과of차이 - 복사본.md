---
layout : posts

title : "자바스크립트 for in 과 of 의 차이"

date : 2021-07-16

categories : javaScript

comments : true
---



자바스크립트의 for문 같은 경우 밑에 코드처럼 사용하고 있다.

```javascript
for (초기식; 조건식; 증감식) {
    ...
}
//예시
for (let i = 0; i < top.length; i++) {
    ...
}
```

우리가 흔히 볼수 있는 포문이다.

<br>

또한 반복문으로는 while문도 있다.

```javascript
while(조건식) {
    
}

//예시
let a = 0;
while(true) {
    if (a === 3) {
        break;
    }
    a++;
}
```

<br>

하지만 for의 in 과 of 는 앞서본 것과 조금 다르다.

<br>

### for문 in

for / in 은 해당 객체의 모든 열거할 수 있는 프로퍼티(enumerable properties)를 순회할 수 있도록 해준다.

<br>

자바스크립트 객체 속성들은 내부적으로 숨겨진 속성들을 가지고 있다. 

그중 하나가 `[[Enumerable]]`이며 for in구문은 이 값이 true로 세팅 되어 속성들만 반복할 수 있다.

이러한 속성들을 **열거형 속성**이라고 부르며, 객체의 모든 내장 메서드를 비롯해 각종 내장 프로퍼티 같은 비열거형 속성은 반복되지 않는다.

<br>

쉽게 말해서 열거형 속성들을 하나씩 순차적으로 접근할 수 있다는 얘기이다.

```javascript
for (let 변수 in 객체) {
    ...
}
    
let shop = {
    name1 : 10,
    name2 : 20,
    name3 : 30
}
    
//예시
for (let name in Shop) {
    console.log(name)        // name1, name2, name3
	console.log(shop[name]); // 10 , 20 , 30
}
```

 <br>

### for문 of

for / of 는 ES6에 추가되었으며, 반복할 수 있는 객체(iterable objects)를 순회할수 있도록 해주는 반복문이다. 

for / of 를 사용하기 위해선 컬렉션 객체가 `[Symbol.iterator]` 속성을 가지고 있어야 한다.

<br>

즉, Array, Map, Set, arguments 등의 객체(Symbol)는 가능하나 Object 같이 다른 타입은 불가능하다.

또한 ES6이므로 현재 익스플로러를 지원하지않는다.

<br>

```javascript
for (let 변수 of 객체) {
    //...
}

//예시
let obj = {
    a : 1,
    b : 2
}
let arr = [1, 2, 3];
for (let el of obj) {
    console.log(el) //error
}

for (let el of arr) {
    console.log(el); //1, 2, 3
}
```

<br>

### for문 in 과 of 의 차이

for / in은 객체의 모든 열거 가능한 속성에 대해 반복하는 것에 반해, for / of는 `[Symbol.iterator]`를 가진 컬렉션만 가능하다.

<br>

<br>

#### Reference

[https://yjshin.tistory.com/](https://yjshin.tistory.com/entry/JavaScript-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-for-%EB%AC%B8-for-in-%EB%AC%B8-for-of-%EB%AC%B8)

https://jsdev.kr/t/for-in-vs-for-of/2938
