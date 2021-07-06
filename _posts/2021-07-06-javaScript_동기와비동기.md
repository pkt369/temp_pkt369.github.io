---
layout : posts

title : "동기와 비동기"

date : 2021-07-06

categories : javaScript

comments : true
---



동기는 **직렬적**으로 처리하는 방식을 말한다.

프로그래밍으로 말하면 하나씩 우리가 만든 코드들을 해치워 나간다는 뜻이다.

이것은 작업을 끝내지못하면 다음 작업으로 넘어가지 못한다는 뜻이다. 이것을 **블로킹**이라고 한다.

<br>

비동기는 **병렬적**으로 처리하는 방식을 말한다.

프로그래밍으로 말하면 우리가 만든 코드를 기다리지않고 다음작업도 바로바로 수행한다는 뜻이다.

<br>

그럼 다들 보통은 이렇게 말한다. '그럼 동기를 안쓰면 되지 않나요?'

그렇다 보통은 쓰지 않는다.  그럼 어떨때 쓸까?

<br>

먼저 기본적으로 자바스크립트는 비동기로 돌아간다. 

만약 우리가 api로 어떤 데이터를 받아오기로 하고 그 데이터가지고 화면에 뿌려주는 작업을 하기로 했다면 비동기로 코드를 짜면 어떻게 될까?



```javascript
function getData() {
	let data = [];
	$.get('https://localhost.com/search/name', function(res) {
		data = res.data;
	});
	return data;
}

view(getData());
console.log(getData()); //undefined
```

<br>

여기서 view에서 얻어온 데이터는 무엇일까? 

![비동기요청](https://user-images.githubusercontent.com/66049273/124543868-03178880-de61-11eb-9163-acbab92e4cb6.jpg)

요청을 하고 나서 응답이 오기 전 비동기적으로 먼저 view가 실행된다.

그럼 view가 가져온데이터는 아무것도 없는 undefined를 얻게 된다.

그럼 여기서는 어떻게 해결해야할까?

그렇다 아마 다들 예상했듯이 우리가 방금 알아본 동기적인 프로그래밍으로 해결하면 된다.

<br>

<br>

<h4>콜백함수</h4>

콜백(callback)함수는 우리가 만든 로직이 끝났을때 원하는 코드를 동작시키는 것입니다.

```javascript
$.get('https://localhost/search/1', function(res) {
    auth(res, function(data) {
        view(res);
    });
});
```

이렇게 우리가 api를 이용하여 데이터를 얻어왔을때 auth를 실행시키고 auth가 끝이 났을때 view를 실행시켜줘라는 뜻입니다.

<br>

만약 여기서 무언가를 더 코딩을 해야한다면 코드들이 들여쓰기가 되고 가독성이 나빠지겠죠?

이런것들을 **콜백지옥**이라고 부릅니다.

<br>

콜백 지옥을 해결방법에는 Promise 나 async await이 있으나 쉽게 해결하는 방법에는 함수를 외부로 빼는 방법입니다.

```javascript
function auth(res) {
	let data = res.ret.data;
    view(data);
}

function view(data) {
    console.log(data);
}

$.get('https://localhost/search/1', function(res) {
    auth(res);
});
```

이렇게 하면 쉬워보이겠지만 함수가 두개만 사용해서 그렇다.

만약 연속해서 함수가 5개 넘어간다면? 가독성이 엄청 떨어지게 될것이다. 

필자가 추천하는 것은 Promise나 async이다.













