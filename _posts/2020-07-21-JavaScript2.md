---

layout : posts

title : "자바스크립트 문법 정리2"

date : 2020-07-21

categoris : JAVASCRIPT

---

앞에 자바스크립트 1편을 못보신분은 [JavaScript 1편](https://pkt369.github.io/JavaScript1/) 여기로 들어가시면 됩니다.

<h4>기본 내장 객체</h4>

**Object 객체** :
 - `toString()`메소드 : 객체를 문자열로 변환할때 자동으로 호출  
 자바에서는 주로 오버라이딩이라고 하는데 `toString()`을 재정의할 수 있습니다.  
  `toString:function(){return this.name + " : " + this.grade}`

 <br>


**Number 객체** :
 - MAX_VALUE : 자바스크립트의 숫자가 나타낼 수 있는 최대 숫자.
 - MIN_VALUE : 최소 숫자.
 - NEGATIVE_INFINITY : 음의 무한대 숫자.
 - POSITIVE_INFINITY : 양의 무한대 숫자.
 - NaN : 자바스크립트 숫자로 나타낼 수 없는 숫자.
 - toString() : 진법값을 리턴(진법값 : 사용할 수 있는 숫자의 갯수와 자리값)
 - toFixed() : 고정 소수점 방식

 <br>


**String 객체** : `var a = "hello"`

<br>


**length 속성** : :문자열 길이

<br>


**메서드 체이닝(Method Chaining)** : 메서드가 반환하는 객체의 값에서 또 다른 함수 호출을 하는 것

<br>


**Array 객체** : 배열

<br>


**Date 객체** : 날짜 - 자바와 비슷

<br>


**Math 객체** : 생성자 함수를 사용하지 않는 객체. 하나의 자료형이므로 변수에 저장해서 함수로 쉽게 사용가능

<hr>

<h4>브라우저 객체 모델(BOM:Browser Object Model)</h4>

: 웹브라우저와 관련된 객체의 집합을 의미.

**window 객체** : 브라우저 기반 자바스크립트의 최상위 객체.
- alert(), prompt() 함수 모두 window 객체의 메서드.
- window 객체의 윈도우 생성 메서드. : `window.open()`

<br>

**screen 객체** : 웹브라우저의 화면이 아니라 운영체제 화면의 속성을 가지는 객체.  
속성보는 방법 :
```java
var output = '';
for(var key in screen){
	output += '※ '+key+':'+screen[key]+'\n';
}
```
<br>

**location 객체** :
- 브라우저의 주소 표시줄과 관련된 객체.
- 프로토콜의 종류, 호스트 이름, 문서 위치등의 정보를 가짐.
- 페이지를 이동할 때 많이 사용.

**페이지 이동 방법 4가지**
-location = 'http://www.daum.net';
-location.href = 'http://www.daum.net';
-location.assign('http://www.daum.net');
-location.replace('http://www.daum.net'); -> 뒤로 가기 버튼을 사용할 수 없음.

**페이지 새로고침**
-location = location;
-location.href = location.href;
-location.assign(location);
-location.replace(location);
-location.reload();

<br>

**navigator 객체** : 웹페이지를 실행하고 있는 브라우저에 대한 정보를 가짐.  
확인 해보기
```java
var output = '';
for(var key in navigator){
  output += '※ '+key+':'+navigator[key]+'\n';
}
```
<br>

**window의 onload 이벤트 속성**(중요) : window 객체가 로드가 완료되고 자동으로 할당된 함수를 실행.
```java
window.onload = function(){
alert('Hello JavaScript onload Event...');
};
```

<br>

위에서부터 내려오는 것이 정석이지만, 그전에 스크립트를 먼저 실행시킨 뒤 위에서 부터 실행됩니다.  

스크립트는 이름이 명시되어저 있는 선언적 함수를 말합니다.  

window.onload는 body가 위도우상에 다 전달이 되어진 뒤 실행합니다.  

그러나 실행시켜보면 alert부터 나옵니다. 전달이 되어진것뿐이지 아직 실행된것이 아니라서 그렇습니다.

<hr>

<h4>문서객체모델(DOM, Document Object Model)</h4>

- 넓은 의미:웹브라우저가 HTML 페이지를 인식하는 방식.
- 좁은 의미:document 객체와 관련된 객체의 집합.
- HTML 페이지에 태그를 추가, 수정, 제거할 수 있음.
- 보통은 jQuery를 통해 사용. 추후 포스팅 예정

* DOM 관련 용어
  - 문서 객체:html or body 태그를 자바스크립트에서 이용할 수 있는 객체로 만들면 그것이 문서 객체.
  - 노드: 각 요소(head, body, title, script, h1, HEADER ...)
  . 요소노드(Element Node):HTML 태그.
  . 텍스트노드(Text Node) : 요소노드 안에 들어 있는 글자.
  - 정적으로 문서 객체를 생성한다의 의미
  : 웹페이지가 처음 HTML 페이지에 적혀있는 태그들을 읽으며 생성하는 것.
  - 동적으로 문서 객체를 생성한다의 의미
  : 자바스크립트를 사용해 원래 HTML 페이지에는 없는 문서 객체를 생성하는 것.

**문서객체생성** :
* 방법1
  - 문서 객체생성
   `var header = document.createElement('h2');`  
   //h2에 접근을 할수있게 해준다. css에서의 접근자와 같은 개념이다.
  - 노드(요소/텍스트) 연결
   `header.appendChild(textNode);` - appendChild : body맨뒤에 넣어주겠다는 뜻
  - body 문서 객체에 header 문서 객체를 추가
   `document.body.appendChild(header);`

<br>

* 방법2
  - 문서 객체의 innerHTML 속성 사용해 객체 생성.
   `document.body.innerHTML += '<h1>Document Object Model</h1>';`

   <br>

**문서객체가져오기** :
 - 웹페이지에 이미 존재하는 HTML 태그를 자바스크립트로 가져오는 방법.
 - getElementById() 메서드는 한 번에 한가지 문서 객체만 가져올 수 있다.
* 방법1
  - getElementById 사용  
  `var header1 = document.getElementById('header_1');`  
  - `getElementsByTagName('tagName')`: tagName과 일치하는 문서 객체를 배열로 가져옴. ex) h1, h2, ...
  - `getElementsByName(name)` : 태그의 name 속성이 name과 일치하는 문서 객체를 배열로 가져옴.
  - `getElementsByClassName('className')`

참고) 바디영역 안 선언 `<h1 id="header_1" class="" name="">HEADER-2</h1>`

<br>

**객체 스타일 조작** :
- `var header = document.getElementById('header_1');` -> `header.style.color=`

**문서 객체 삭제** : 일반적으로 문서 객체를 제거 할 때 사용하는 코드.
```java  
var willRemove2 = document.getElementById('header_2');
willRemove2.parentNode.removeChild(willRemove2);
```

원래는 2편으로 끝낼려했지만 생각보다 길어져 3편까지 포스팅하기로 했습니다.
3편 포스팅은 다음에 하겠습니다.

1편은 여기로 -> [JavaScript 1편](https://pkt369.github.io/JavaScript1/)
