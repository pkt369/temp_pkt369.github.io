---

layout : posts

title : "html 기본 문법 정리"

date : 2020-07-13

categoris : HTML

---

공부했을때 적어놓은 것들을 위주로 짧게 정리해보았다.

html은 기본 뼈대라고 했다.

기본 뼈대를 튼튼히 세우기위해 html도 열심히 공부하자.

html 뿐만아니라 css도 정리해놓은게 있어서 다음 블로그 포스팅에 적을 생각이다.


**주석문** `<!-- -->` :

	ctrl + shift + /

**큰제목, 글자태그(제목), HeaderTag** :

	<h1></h1> ~ <h6></h6>

**일반글, 글자태그(본문), paragraphTag** :

	<p></p>

**수평줄** :

	<hr> (단일태그)

**줄바꿈** :

	<br>`(단일태그)

**anchorTag** :

	<a href=””></a> : 웹페이지 이동

**anchorTag2** : 다른곳에서 아이디 만듦

	ex) <h1 id=alpha> -> <a href=”#alpha”> </a> : #ID

**흐르는 문자열, marquee** :

	<marquee behavior=”slide” = 슬라이드 문자(끝에가면 멈춤)
	<marquee behavior=“alternate” = 좌우 이동 문자열
	입력X(디폴트값) 흐르는 문자열(끝까지 가면 앞에서 다시나옴)
**목록 기반 태그, listTag** : 	

	<ol><li></li></ol> : ordered list : 번호가 있는 목록 태그
			<ul><li></li></ul> : unordered list : 번호가 없는 목록 태그

**정의 목록 태그, defListTag** :

	<dl><dt><dd>내용</dd>(들여쓰기로된 일반 문장)</dt>(제목)</dl>(큰틀)

**테이블 태그, tableTag** :

	<table border=”1”(테두리크기)><tr><td></td>(행)<</tr>(열)</table>

**이미지 태그, imageTag** :

	<img alt=””(이름) src=”./images/Tulips.jpg”(경로) (단일태그)

**오디오 태그, audioTag** :

	<audio controls autoplay loop><source src=”./content~type=””></audio>

**비디오 태그, videoTag** :

	<video src=””controls=””autoplay=””,loop=””></video>

**Label 태그** :

	<label></label>

**Textarea 태그** :

	<textarea row=”” cols=””></textarea> : cols=태그의 너비,rows=태그의 높이

**selectTag** :

	<select>여러 개의 옵션:<option></option><select>

**selectTag2** :

	<select><optgroup label=””><option></option><optgroup>>
	<optgroup label=””><option></option><optgroup></select>
	(opt로 그룹나누기)

**Fieldset & legend 태그** :

	<fieldset><legend></legend>~~(내용)<fieldset> : 입력양식을 설명하는 태그.

**공간분할태그, divTag** :

	<div>~</div> : block 형식으로 공간을 분할. 차곡차곡 쌓아 올려지는 형식

**Block 형식** :

	div태그/ h1~h6태그 / p태그 / 목록태그(ol, ul, li) / 테이블태그 / form태그

**공간분할태그, spanTag** :

	<span>~</span> : inline 형식으로 공간을 분할, 한줄안에 차례차례 위치하는 형식.

**Inline 형식** :

	span태그 / a태그 / input태그 / 글자형식태그

**HTML5 시멘틱 구조 태그** :  


	버전1 : <div=”Header”>,<div id=”Main Menu”>, SubMenu, Contents, Footer


<hr>

	버전2 : div없이 <header>,<nav>
	
	<header> : 헤더를 의미한다(회사명/로고)
	<nav> : 네비게이션을 의미(주메뉴 구성)한다.
	<aside> : 사이드에 위치(sub 메뉴/광고)하는 공간을 의미한다.
	<section> : 여러 중심 내용을 감싸는 공간을 의미한다.
	<article> : 글자가 많이 들어가는 부분을 의미한다.
	<footer> : 맺음말(이용약관|주소(위치)|저작권|사이트맵)을 의미한다.


**문단정렬태그, pre & xmp Tag**  :

	<pre></pre> : pre사이에 있는 띄워쓰기, 엔터 모두 인식한다.

**xmp태그** :

	<xmp></xmp> : xmp사이에 있는 태그를 인식하지 않는다.

**metaTag** :

	<head><meta charset=”UTF-8”><meta http-equiv=”Content-Type”~~></head>
	: 정보를 입력하기위해 쓰는 태그.
