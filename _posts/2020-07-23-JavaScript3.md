---

layout : posts

title : "자바스크립트 문법 정리3"

date : 2020-07-23

categoris : javaScript

---

자바스크립트 문법시리즈는
- [자바스크립트 문법정리 1편](https://pkt369.github.io/JavaScript1/)
- [자바스크립트 문법정리 2편](https://pkt369.github.io/JavaScript2/)

오늘은 자바 문법시리즈 마지막편입니다.

<hr>

<h4>이벤트</h4>

- load : 이벤트 이름 or 이벤트 타입
- onload : 이벤트 속성
- 이벤트 핸들러 or 리스너 : 이벤트 속성에 할당된 함수.
- 이벤트 모델 : 문서 객체에 이벤트 연결하는 방법.
- 이벤트 연결: window 객체의 onload 속성에 함수 자료형을 할당하는 것.

```java
window.onload = function(){
  var header = new document.getElementById('header');

		function whenClick(){
			alert('CLICK');
		}

		header.onclick = whenClick;
}
```

`window.onload`는 바디영역이 모두 다 전달을 끝냈을 때 실행되는 함수이다.

`.onclick`은 그 영역이 클릭됐을 때 실행되는 함수이다.

```java
window.onload = function(){
  document.body.onclick = function(e){
    // 이벤트 객체를 설정
    var event = e || window.event;

    document.body.innerHTML = '';
    for(var key in event){
      document.body.innerHTML
      += '<p>'+key+' : '+event[key]+'</p>';
    }
  };
};
```

`var event = e || window.event;` : e가 존재하면 e를 변수 event에 넣고, e가 undefined이면 window.event 속성을 변수 event에 넣는다.  
e 와 window.event는 일어난 이벤트에 대한 정보를 가지고 있다.  
브라우저에 따라서 e를 줄지 window.event를 줄지 다른것이지 같은 개념이다.

<br>

**기본 Event제거**
- 일부 HTML은 이미 이벤트 헨들러를 가지고 있음.
```java
window.onload = function(){
// 이벤트 연결
  var form = document.getElementById('my_form');

  form.onsubmit = function(){ //버튼이 눌릴때
    var pass = document.getElementById('pass').value;
    var pass_check = document.getElementById('pass_check').value;

    if(pass == pass_check){
      alert('회원가입성공');
    }else{
      alert('비밀번호를 확인하세요....');
      return false; // 이미 가지고 있는 이벤트 핸들러 제거됨.
    }
  };
};
```

비번과 비번확인 틀릴때 이벤트를 제거해서 버튼이 가지고 있는 이벤트(전체의 정보를 다음으로 넘어가는 것)를 없애는 것이다.

<br>


**이벤트 전달**
- 이벤트 버블링 방식이 **일반적**
  * 자식노드에서 부모 노드 순으로 이벤트 실행.
- 이벤트 캡쳐링
  * 이벤트가 부모 노드에서 자식 노드 순으로 실행되는 것.
```java
  window.onload = function(){
		document.getElementById('header1').onclick = function(e){
			alert('header');
		};

		document.getElementById('paragraph1').onclick = function(e){
			var event = e || window.event; // IE8 이하 버전...
			alert('paragraph');

			// 이벤트 전달 제거
			event.cancelBubble = true; // IE8 이하 버전...
			if(event.stopPropagation){
				event.stopPropagation();
			}
		};
	};
```

참고) header1이 부모 노드이고, paragraph1이 자식 노드이다.

컴파일해서 보면 alert(header)은 뜨지 않는 것을 볼수 있다.

<hr>

<h4>예외 처리</h4>

- 정의:프로그램이 실행되는 동안 문제가 발생하면 프로그램이 자동으로 중단된다. 이럴 때 프로그램이 대처할 수 있게 처리하는 것.

**기본**
```java
function whenClick(e){
		var event = e || window.event;

		var willAlert = '';
		willAlert += 'clientX: '+event.clientX+'\n';
		willAlert += 'clientY: '+event.clientY+'\n';
		alert(willAlert);
	}
```

예외처리보단 응용에 가까운 코드이다. event를 받아와서 좌표점을 보여주는 코드이다.

**고급**
 1.

```java
      try{
    	  willExcept.byebye();

      } catch(exception) {
    	  alert('예외가 발생');
      } finally {
    	  alert('고급 예외 처리 수행 끝.');
      }
```

이코드는 `willExcept.byebye()`를 만나면 바로 catch로 넘어간다. 그리고 finally는 끝에 무조건 실행되는 코드이다.

2.

- 예외 객체 속성
  - message : 예외메세지
  - description : 예외 설명
  - name : 예외 이름


3.
```java
function divide(alpha, beta){
		if(beta == 0){
			throw 'DivideByZeroException';
		}

		return alpha/beta;
	}

    try{
    	divide(10, 0);
    }catch(exception){
    	alert('CATCH');
    }
```

이코드는 예외를 강제로 발생시키는 코드이다.

<hr>

<h4>외부 자바스크립트 사용</h4>

사용하는 방법은 간단합니다.

바로 코드를 보여드리겠습니다.

```java
<script src="./js/ExternalJScript.js"></script>
<script type="text/javascript">
	alert(typeof(externalFileFunction));
	alert(typeof(externalFileVariable));
</script>
```

바로 `<script src="./js/ExternalJScript.js"></script>`가 핵심이다.
src에 외부에있는 자바스크립트 주소값을 넣어주기만 하면 외부에서 있는 함수들을 사용할 수 있습니다.

자바스크립트 문법시리즈는
- [자바스크립트 문법정리 1편](https://pkt369.github.io/JavaScript1/)
- [자바스크립트 문법정리 2편](https://pkt369.github.io/JavaScript2/)
