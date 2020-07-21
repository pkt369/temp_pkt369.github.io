---

layout : posts

title : "자바스크립트 문법 정리"

date : 2020-07-20

categoris : JavaScript

---

자바 스크립트는 자바와 비슷한 문법으로 웹을 꾸밀때 사용되는 언어이다.

html, css, JavaScript 총 3개가 프런트개발자의 대표적인 언어이다.

그리고 JavaScript는 **동적** 인 이벤트에 많이 사용된다.

바로 기본 문법으로 들어가보자.

**주석문** : `//`, `/* */` -> 자바와 같음(단축키 : ctrl+shift + /)

**알림창** : `alert("내용")` -> 팝업창에 내용이 뜸

**자바스크립트는 대문자와 소문자 구분이 없다.**

`alert("Hello, \"World\" ")` : **자바와 같이 똑같이 이스케이스 시퀀스가 사용가능하다**

**변수** : `var` -> 자바와 달리 스크립트는 var로 모든 변수를 선언할수 있다.

**자료형 검사** : `typeof(exam)` -> 무슨 타입인지 가르쳐준다 ex) string, number, 선언x : undefined

**입력** : `prompt('이름을 입력하세요.','두 글자 이상 입력')`
![prompt](https://user-images.githubusercontent.com/66049273/88000457-a4b2a680-cb38-11ea-9fe8-3855b4e633bb.png)

boolean으로 입력 받기 : `confirm()`

**자료형변환** :
* 덧셈 : `alert(12+345)` -> 357, `alert(12 +'345')` -> 12345, `alert('12' + '345')` ->12345
* 덧셈을 제외한 나머지 사칙연산 : alert('12' * 3) -> 36 : 문자열이어도 숫자로 변환.

**강제자료형변환** : 숫자 -> `Number(input)`, 문자열 -> `String(input)`

**산술연산자** : `+, -, *, /, %`

**비교연산자** : `<, >, <=, >=, ==, !=`

**논리연산자** : `&&, ||, !`

**배열** : `var array = [123, 'string', 'true', function(){}];` -> 배열에는 모든지 다 들어갈 수 있다.

**if문** : `if(a > b){}` -> 자바와 같다.

**switch문** : `switch(i % 2 == 0)case: break;` -> 자바와 같다.

**삼항연산자** : `a > 2 : alert(양수) ? alert(음수)` -> 조건 : 참 ? 거짓

**짧은 조건문** : 조건 || false이면 실행, 조건 && true면 실행

<hr>

<h4>반복</h4>

**while** : `while(조건문){}`

**do ~ while** : `do {} while(조건문);` -> while과 다른점은 do~while은 **무조건 한번 실행** 을 하고 조건문을 검사한다.

**for문** : `for(var a = 0; a < 5; a++) {}` -> 포문의 진행 순서 :  
  var a = 0(선언) - a < 5(비교) - {}(내용실행) - a++(연산) - 다시비교 - 내용실행 반복

**for in문** : `for(var a in array){alert(array[a])}`

**break** : 반복문 빠져나가기.

**continue** : 만나면 밑에 내용 실행하지 않고 비교문으로 다시 이동.

<hr>

<h4>함수</h4>

**종류**
* 익명함수 : 이름이 없는 함수
* 선언적함수 : 이름이 있는 함수

**함수 재정의**
* 익명함수 재정의 : `var func = function(){alert('함수')}`  
 !) var func = 이렇게 두번 선언하면 오류가 걸리지 않는것처럼 보이지만 실제로는 오류사항이다.
<br>
* 선언적함수 재정의 : `function move(){alert("함수호출")}`  
 **웹브라우저는 script태그 내부의 내용을 다 읽기전에 선언적함수를 먼저 읽는다.** -> 함수를 먼저 적고 정의를 뒤쪽에 적어도 실행이 된다.

**매개변수** :
* `alert()` : 두번째 매개변수는 무시한다.
* `prompt()` : 두번째 매개변수에 아무것도 쓰지않으면 undefined이 된다.
* `Array()` : 매개변수에 아무것도 없는것이 기본, 빈배열만듦,
* `Array(10)` : 매개변수의 크기를 가지는 배열 생성, `Array(10, 3, 55, 6)` : 매개변수를 가지는 배열 생성

**가변인자** : `function leng() {alert("길이 : " + leng.length);}` -> 매개변수의 갯수가 변할수 있는 함수.

**리턴** : 함수에서 아무값없이 return;하면 함수종료, 값이 있으면 값을 반환한다.

**내장 함수** :
- escape() : 영문 알파벳, 숫자, 일부 특수문자`(@, *, -, _, +, ., /)`를 제외한 모든 문자를 인코딩한다.  1바이트문자는 %XX의 형태로, 2바이트 문자는 %uXXXX의 형태로 변환한다.
<br>
- encodeURI() : .escape() 함수에서 인터넷 주소에 사용되는 일부 특수문자(:, ;, ?, =, &)는 변환하지 않는다.
<br>
-  encodeURIComponent() : 알파벳과 숫자를 제외한 모든 문자를 인코딩한다, UTF-8 인코딩과 같다.
<br>
-  eval(string) : string을 자바스크립트로 실행.
<br>
- isFinite(number) : number가 무한한 값인지 확인.
<br>
- isNaN(number) : number가 NaN(Not a Number:변수)인지 확인.
<br>
- parseInt() 함수 & parseFloat() 함수 : int, float으로 변경 -> 문자부터 시작하면 NaN 반환, 공백무시

<hr>
<h4>Object(객체)</h4>

**객체 생성 - 키:요소** : `var product = { name:"TV", 제조사:"한국" };`, `alert(product.name)` or `alert(product['제조사'])`

**객체 동적 추가/제거** : `var a ={};`,  
  동적으로 추가 `a.student = "학생;"` ,  
  동적으로 메서드 추가 `a.toString = function() {var output = "hi"; return output;}`  
  객체의 속성 제거 `delete(a.student)`

<br>

<h4>생성자</h4>

* new 키워드를 사용해 객체를 생성할 수 있는 함수.
* 생성자 함수를 사용한 객체의 생성과 출력.
* 그냥 함수를 사용해 객체를 리턴하는 방법과 차이가 없어 보임.
exam) `function Student(a, b) = {~~}; var student = []; student.push(new Student(a, b))`
push는 자바의 add와 같은 기능(배열에 값 추가)

<br>

<h4>프로토타입</h4>

생성자 함수를 사용해 생성된 객체가 공통으로 가지는 공간(자바의 static)
`Student.prototype.getSum = function(){ return this.국어+this.수학+this.영어+this.과학; };`

<br>

<h4>instanceof 키워드</h4>

- 인스턴스:생성자 함수를 통해 만들어진 객체.
- 해당 객체가 어떠한 생성자 함수를 통해 생성됐는지를 확인할 때 사용하는 키워드.  
자바에서는 상속에서 -속성을 알고있는지 확인할때 사용함.

<br>

<h4>상속</h4>

- 생성자 함수를 선언.
- 자바처럼 구체적이지않고 사실상 상속의 개념이 없다고 봐도 무방하다. - 정해지지않음.
- 첫글자를 대문자로하면 생성자로 하겠다는 프로그래머들의 약속이 있다.
```JavaScript
function Rectangle(w,h){
    var width = w; //지역변수, 필드로 선언이 되고 싶으면 this.을 써야한다.
    var height = h;

    this.getWidth = function() {return width;}
    this.getHeight = function () {return height;}

    this.setWidth = function(value){
      if(value < 0){
        throw '길이는 음수일 수 없습니다.';
      } else {
        width = value;
      }
    }
    this.setHeight = function(value){
	    	if(value < 0){
	    		throw '길이는 음수일 수 없습니다.';
	    	} else {
	    		height = value;
	    	}
	   }
  }
  Rectangle.prototype.getArea = function () {
      	return this.getWidth() * this.getHeight();
  }

  function Square(length){
    	this.base = Rectangle;
    	this.base(length, length);
  }
  Square.prototype = Rectangle.prototype;

  var rectangle = new Rectangle(5, 7);
  var square = new Square(5);

  alert(rectangle.getArea());
  alert(square.getArea());
```

상속 말만 쓰면 어려울것같아서 코드로 대체했다.

다음은 조금더 심화되고 동적인 자바스크립트의 포스팅을 할것이다.
