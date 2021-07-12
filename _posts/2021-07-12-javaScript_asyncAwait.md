---
layout : posts

title : "async await"

date : 2021-07-12

categories : javaScript

comments : true
---



저번 포스팅 중에서 [Promise](https://pkt369.github.io/javascript/javaScript_Promise/)에 대해 포스팅을 한적이 있다. 

Promise는 동기처럼 기다렸다가 결과값을 받아오면 then으로 결과값으로 받아서 로직을 구성하고, 이전 코드들과 다르게 Promise는 콜백 지옥에서 벗어날 수 있다 로 정리할 수 있다.

그럼 이번 포스팅에서는 async await에 대해 포스팅해보겠다.

<br>

### async await

ES8의 공식 스펙으로 비동기 코드를 동기식으로 쓸 수 있도록 도와주며, async await을 사용하면 비동기 코드를 작성할때처럼 명확하게 코드를 쓸수 있다.

<br>

async await은 function 앞에 async를 붙여주고, 기다려야 할 함수앞에 await을 붙여주면 사용할 수 있다.

```javascript
async function a() {
    await getData();
}
```

async를 예약어라고 부르며, 여기서 주의해야할 점은 getData가 프로미스 객체를 반환해야 await이 잘 작동된다.

즉, Promise와 async await 은 한 세트이다.

<br>

좀더 이해를 돕기 위해 예제를 보자

```javascript
function getData(params) {
    return new Promise(function(resolve, reject) {
        $.ajax({
            $.ajax({
                url: "/getData",
                type: 'GET',
                data: {'params': params},
                dataType: 'json',
                contentType: 'application/json',
                success: function (res) {
                    resolve(res);
                },
                error: function (e) {
                    reject(e);
                }
            }, true);
        });
    });
}

function a() {
	let params = getParams(); //쿼리 파라미터 얻어오는 함수
    getData(params)
    	.then(function (res) {
        	view(res);
    	});
}

async function a() {
	let params = getParams(); //쿼리 파라미터 얻어오는 함수
	let res = await getData(params);
    view(res.body);
}
```

Promise를 먼저 선언을 하고  async await을 통해 동기를 비동기처럼 코드를 작성한 것을 볼수 있다.

<br>

위의 a 코드와 밑의 a코드를 비교해보길 바란다.

위의 a 코드 같은 경우는 들여쓰기가 생기면서 한눈에 들어오지 않는 단점이 있다.

아래의 a 코드 같은 경우 우리가 비동기방식으로 쓰던 것처럼 코드를 작성해서 좀더 이해하기 쉽고 한 눈에 잘들어온다.

<br>

### 예외처리

async await은 try catch로 예외 처리를 한다.

```javascript
async function a() {
    try {
        let params = getParams(); //쿼리 파라미터 얻어오는 함수
        let res = await getData(params);
   		view(res.body);
    } catch (e) {
        console.error(e);
    }
}
```

우리가 이전 Promise에서 봤던 catch랑 같다고 생각하면 된다.

catch는 네트워크 통신뿐만 아니라 발생하는 모든 에러를 잡아내기때문에 유형에 맞는 에러코드 처리를 해주면 된다.

