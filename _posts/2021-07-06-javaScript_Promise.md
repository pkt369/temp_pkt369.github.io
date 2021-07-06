---
layout : posts

title : "자바스크립트 Promise"

date : 2021-07-06

categories : javaScript

comments : true

---



자바스크립트에서 비동기 처리를 먼저 알아야 Promise를 제대로 이해할수 있다.

[동기와 비동기](https://pkt369.github.io/javascript/javaScript_%EB%8F%99%EA%B8%B0%EC%99%80%EB%B9%84%EB%8F%99%EA%B8%B0/)를 우선적으로 이해하기를 바란다.

<br>

<br>

<h3>Promise</h3>

promise는 비동기적인 로직에서 시간이 필요한 로직이 응답이 올때까지 기다렸다가 응답이 온뒤에 로직이 실행되는 것을 의미한다.

기본 콜백함수는

```javascript
function getData() {
    $.get('https://localhost.com/search/1', function(res) {
        view(res);
    });
}
```

이렇게 짜던 것에 비해

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
		$.get('https://localhost.com/search/1', function(res) {
        	resolve(res);
	    });
    });
}

getData().then(function (res) {
    view(res);
});
// getData().then(view(res));
```



이렇게 표현이 가능해졌다.

여기서 new Promise(), resolve(), reject()는 뭘까?

<br>

<br>

<h3>프로미스의 3가지 상태(status)</h3>

먼저 프로미스의 상태는 3가지가 있다. 상태란 Promise를 처리하는 과정을 말한다.

1. Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
2. Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
3. Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

<br>

<h5>Pending(대기)</h5>

new Promise를 호출하면 대기(Pending) 상태가 된다.

인자로는 콜백함수인 resolve와 reject를 선언 할 수 있다.

<br>

<h5>Fulfilled(이행)</h5>

만약 성공적으로 응답이 왔을 경우 콜백함수인 resolve 를 실행시키는데 이를 이행(FulFilled)상태라고 한다.

그리고 이행 상태가 되면 .then() 을 통해서 처리 결과값을 받을 수 있다.

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
        resolve(1);
    });
}

getData().then(function (res) {
	console.log(res); // 1
});
```

<br>

<h5>Rejected(실패)</h5>

new Promise()에서 실패하거나 에러를 낼 경우 콜백 함수인 reject함수가 호출 됩니다.

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
		reject(new Error("api Error"));
    });
}

getData().then(function (res) {
	console.log(res); // 1
}).catch(function(e) {
    console.error(e);
});
```

<br>

<br>



<h3>Promise Chaining(프로미스 연결)</h3>

프로미스의 또다른 특징은 프로미스를 연결하여 사용할 수 있다는 점이다.

then()을 호출할 경우 새로운 프로미스 객체가 반환이 된다. 

그러면 프로미스 객체는 또 then()을 할수 있다

```javascript
getData().then(function (res) {
	view(res);
}).then(function() {
    //...
}).then(function() {
    //...
});
```

<br>

응용을 하면 이렇게된다.

```javascript
function getData() {
    return new Promise(function (resolve, reject) {
		resolve(res);
    });
}

getData()
    .then(auth)
	.then(filter)
	.then(view);
```

설명을 하자면 auth, filter, view는 직접 만든 함수이며, 얻은 데이터가지고 auth 체크하고 데이터를 거른뒤에 view 해달라는 코드이다.

<br>

콜백 지옥을 경험했다면 이런 코드가 이전보다 가독성이 좋아진 것을 느낄수 있을 것이다.

<br>

<br>



<h3>Promise의 두가지 Error처리</h3>

먼저 앞서 얘기드리자면 catch를 사용하여 에러처리를 하는 것이 좋다.

그이유는 밑에서 설명 드리겠다.

<br>

1. catch
2. then()의 두번째 인자

이렇게 두가지가 있다.

<br>

```javascript
// 1.
getData().then().catch();

// 2.
getData().then(function (res) {
	console.log(res);
}, function (e) {
	console.error(e);
});
```

위와 같이 두가지를  쓸수 있으나 catch를 써야한다고 말씀드리고 싶다.

그 이유는 만약 then()에서 첫번째 인자에서 에러가 날 경우 두번째 인자에서는 첫번째 인자의 에러를 잡지 못하기 때문이다.

```javascript
getData().than(function (res) {
    new Error("error");
}, function (e) {
    console.error(e);
}); //Error in then
```

<br>

<br>

<h3>마무리</h3>

회사에서 일을 하다보면 Promise와 async await을 많이 사용하는데 제대로 알지못해서 불필요한 곳에 썼던 적이 있다.

그렇기 때문에 공부를 해야한다고 느껴졌고 공부를 하면서 좀더 자세히 알게되어 뿌듯했다.

요즘 웹에서 많이 사용하는 것들은 그냥 쓰지말고 공부를 좀더 하고 써야한다는 깨달음을 얻기도 했다.



다음글은 async await 을 공부하면서 적어볼 예정이다.

<br>

참고한 블로그 : [캡틴판교님 블로그](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)









