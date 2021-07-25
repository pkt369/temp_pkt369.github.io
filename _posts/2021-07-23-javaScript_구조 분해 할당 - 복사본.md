---
layout : posts

title : "자바스크립트 구조 분해 할당"

date : 2021-07-23

categories : javaScript

comments : true
---



MDN 에서는 구조 분해 할당이란 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 자바스크립트라고 표현하고 있다.

말그대로 하나씩 분해해서 하나씩 넣어준다는 뜻으로 볼수있다.

```javascript
let a, b, c;
[a, b, c] = [1, 2, 3];
//========================
a = 1;
b = 2;
c = 3;
```

<br>

### 배열 구조 분해 할당

```javascript
let a, b, arr;
[a, b] = [10, 20];
console.log(a); //10
console.log(b); //20

[a, b, ...arr] = [10, 20, 30 ,40 ,50];
console.log(arr); //30, 40, 50

[a = 1, b = 2] = [null]; //[a = 1, b = 2] = [null, undefined]
console.log(a); //null
console.log(b); //2
```

우리가 기존에는 `let a = 10`이런 코드랑 틀리다는 것을 볼수 있다.

그리고 `...arr`을 통해 배열을 삽입할수도 있다는 것을 알 수있다.

<br>

맨마지막을 보면 null 값을 넣어줄수 있음을 알수 있고, 분해한 값에 맞는 인덱스만 값을 넣어준다는 것을 알수있다.

또한 **분해한 값이 undefined일 경우 원래 값을 사용**하게 된다.

<br>

#### 변수 값 교환하기

```javascript
let a = 1;
let b = 2;
[a, b] = [b, a];
console.log(a); //2
console.log(b); //1
```

<br>

#### 일부 값 받지 않기

```javascript
function f() {
    return [1, 2, 3];
}

let [a, , c] = f();
console.log(a); //1
console.log(c); //3
```

<br>

#### 객체 구조 분해 할당

배열과 비슷하며 한 element를 했던 것에 반해 객체는 키와 값 즉, 하나의 엔트리를 기준으로 분해한다.

<br>

#### 선언 없는 할당

```javascript
let a, b;

({a, b} = {a: 1, b: 2});
// a = 1, b = 2
//[a, b] = [1, 2];
```

선언 없이 객체 리터럴 비구조화 할당을 사용할땐 () 를 이용하여 객체 리터널처럼 사용한다.

만약 ()를 사용하지 않고 `{a, b} = {a: 1, b: 2}`일 경우 {a, b}가 블록(Block Scope)으로 간주되어 안에서만 접근 할수 있게 된다. 즉, a, b는 =의 오른쪽 a와 대입할수 없다는 뜻이다.

<br>

참고) 비구조화 할당이란

- 객체같은 구조에서 데이터를 가져오는 것이다.

  ```javascript
  let foo = {a: 1, b: 2, c: 3};
  let {a, b, c} = foo;
  ```

  선언하는 a 와 오른쪽의 키와 같으면 값을 대입해주는 것을 비구조화 할당이라고 한다.

<br>

#### 새로운 변수에 할당하기

```javascript
let {a: age, n: name} = {a: 5, n: "test"};
console.log(age); //5
console.log(name); //test

let {a: aa = 1, b: bb = 2} = {a: 10};
console.log(aa); //10
console.log(bb); //2;
```

<br>

#### undefined가 있으면 원래 값 할당

```javascript
let {a: 5, b: 6} = {a: 3};
console.log(a); //3
console.log(b); //6
```

<br>

### 응용하기

위에서 기본을 배웠으니 응용해서 써볼려고 한다.

```javascript
let user = {[
        id: 1,
        name: "test1",
        age: "25",
        address: "Seoul"
    ],[
    	//...        
    ]
}

//안좋은 예
function userLog1(user) {
    consloe.log(`${user.name}은 나이가 ${user.age}이며 주소는 ${user.address}이다.`);
}

//좋은 예
function userLog2({name, age, address}) {
    consloe.log(`${name}은 나이가 ${age}이며 주소는 ${address}이다.`);
}

function userLog3(user) {
    const {name, age, address} = user;
    consloe.log(`${name}은 나이가 ${age}이며 주소는 ${address}이다.`);
}

```

기존에 썼었던 코드에는 user.을 반복하면서 같은 변수를 계속 쳐주고 있었다.

우리가 위에서 배웠던 구조 분해 할당 (비구조화 할당)을 함으로써 새로운 변수에 값을 넣어준 것을 알수있다.

<br>

#### Reference

https://developer.mozilla.org/ko/docs/orphaned/Web/JavaScript/Reference/Operators/Destructuring_assignment

