---

layout : posts

title : "Express모듈을 통한 서버의 코드 리뷰"

date : 2020-08-13

categoris : NODEJS

comments : true

---

nodeJs를 코드리뷰방식으로 공부했던 것을 공유 해볼려고 합니다.

```javascript

const express = require('express');
const path = require('path');

const app = express();
app.set('port', process.env.PORT || 3000); // process.env 객체에 PORT 속성이 있다면 그값을 사용하고,
//없다면 기본값으로 3000번 포트를 이용하도록 함 // SET(키/값) 형태 // 나중에 데이터를 app.get로 가져올 수 있음

app.get('/', (req, res) => {
    // app.get(주소, 라우터) :
    //라우터(데이터를 전송을 위한 최적의 경로 설정하고 한 통신망에서 다른 통신망으로 통신할 수 있도록 도와주는 인터넷 접속 장비))
    //는 주소에 대한 GET 요청이 올 때 어떤 동작을 할지 적는곳

    //req는 요청에 대한 정보, res는 응답에 대한 정보
    //익스프레스에서는 res. write/end 대신 send로 사용

    //res.send('HELLO EXPRESS');
    //만약 HTML을 보내고 싶을시 sendFile을 이용할것

    res.sendFile(path.join(__dirname, '/index.html'));
    // path.join : 인자로 받은 경로들을 합쳐서 문자열로 반환

});
//get 요청외에도 POST, PUT, PATCH, DELETE, OPRTION에 대한 라우터를 위한 app.post, app.put, app.patch, app.delete, app.option
//메서드가 존재함.

app.listen(app.get('port'), () => { //listen은 http웹서버와 동일
    console.log(app.get('port'), '번 포트에서 대기 중');
});
```

<br>
<br>

<hr>

<h3>미들웨어</h3>

```javascript
const express = require('express');
const path = require('path');

const app = express();

app.set('port', process.env.PORT || 3000);

app.use((req, res, next) => { // 미들웨어라고 부르며 위에서부터 아래로 실행됨
    //미들웨어는 요청과 응답사이에 특별한 기능을 추가할수 있는 기능.
    //주소를 넣어주지 않으면 모든 요청에 실행됨

    console.log("모든실행에 다 실행");
    next(); // next를 해줘야 다음 미들웨어가 실행됨.
});

app.get('/', (req, res, next) => {
    console.log("get / 요청에만 실행");
    next();
}, (req, res) => { // 위에 next를 받아서 내려오게됨.
    throw new Error('에러는 에러 처리 미들웨어로 갑니다.'); // 무조건 실행됨.
});

app.use((err, req, res, next) => { // 에러처리 미들웨어라고 부르며 next를 하지않아도 에러가 걸리면
    //여기로 오게된다.

    console.error(err);
    res.status(500).send(err.message);
});

app.listen(app.get('port'), () => {
    console.log(app.get('port'), "포트에서 대기중 입니다.");
});
```

<br>
<br>

<hr>

<h3>다른 모듈들을 사용하기</h3>

```javascript
const express = require('express');
const morgan = require('morgan');
const cookieParser = require('cookie-parser'); // parser : 해석할수 있는 단위로 여러부분으로 분할해주는 기능
const session = require('express-session');
const dotenv = require('dotenv'); //dot(.)+env : .env 파일을 읽어서 process.env로 만듦.
//.env를 별도의 파일로 관리하는 이유는 보안과 설정의 편의성때문이다.
//비밀 키들을 소스 코드에 적어놓으면 코드 유출시 노출됨. -> .env파일 관리로 유출 방지
const path = require('path');

dotenv.config(); //.env안에 있는 파일을 불러오기
const app = express();
app.set('port', process.env.PORT || 3000);

//설치했던 패키지들을 미들웨어에 연결
// (res, req, next)는 미들웨어 내부에 들어가있음. next도 내부적으로 호출하기에 다음 미들웨어로 넘어감.
app.use(morgan('dev'));
// 콘솔창 [HTTP메소드][주소][HTTP상태코드][응답속도]-[응답 바이트]를 의미

app.use('/', express.static(path.join(__dirname, 'public'))); // 폴더를 지정한것
//static 미들웨어는 정적인 파일들을 제공하는 라우터 역할.
// 사용법 : app.use('요청경로', express.static('실제 경로'))
// 사용시 장점 : 요청 경로와 서버 폴더가 다르므로 외부인이 서버의 구조를 쉽게 파악할수 없게 함.
// 정적 파일들을 알아서 제공 -> readFile 사용X
// 요청 경로에 해당하는 파일이 없으면 알아서 내부적으로 next를 호출. 발견했다면 next를 호출하지 않아 다음 미들웨어 실행 X

//body-parser : 요청의 데이터를 req.body 객체로 만들어주는 미들웨어(폼데이터, ajax(페이지 일부만 새로고침기능))
app.use(express.json()); //json형식의 데이터 전달 방식
app.use(express.urlencoded({extended: false})); // false면 querystring 모듈을 사용하여 쿼리스트링을 해석하고,
//true면 qs모듈을 사용하여 쿼리스트링을 해석. qs모듈은 npm패키지이며, querystring 모듈의 기능을 좀더 확장한 모듈이다.
//추가로  Raw(버퍼데이터), Text(문자형식) 형식도 가능


app.use(cookieParser(process.env.COOKIE_SECRET)); // 요청에 동봉된 쿠키를 해석해 req.cookies 객체로 만드는 것
//서명된 쿠키값에 시크릿키를 뒤에 붙여 서버가 검증. // 쿠키를 생성하진 않음
//서명이 붙을시 name=co.sign과 같은 모양이고, req.signedCookies객체에 안에 있음
//process.env.COOKIE_SECRET에 cookiesecret 값을 할당(키=값 형식으로 할당)

// 세션이란 웹통신간 유지할려는 정보를 저장하는 것
//쿠키는 개인PC에 세션은 서버에 저장되는 것이다.
app.use(session({
    resave: false, // 요청이 올때 수정사항이 생기지 않더라도 세션을 다시 저장할지 설정
    saveUninitialized: false, // 세션에 저장 할 내역이 없더라도 처음부터 세션을 생성할지 설정
    secret: process.env.COOKIE_SECRET, // 안전하게 전송하기위에 서명을 해야하고, 쿠키를 서명하는데 screat값이 필요함.
    //cookieParser와 같은 시크릿 키를 써야한다.
    cookie: {
        httpOnly: true, //클라이언트가 쿠키 확인 안되게 하는것
        secure: false, // https가 아닌 환경에서 사용가능
    },
    name: 'session-cookie', //기본 이름은 connect.sid
}));
//세션쿠키를 넘겨줘서 클라이언트가 받고 request를 할때 서버에줘서 서버가 받은정보를 토대로 정보를 넘겨준다.

app.use((req,res,next) => {
    console.log('모든요청에 들어갑니다');
    next();
});

app.get('/', (res, req, next) => {
    console.log('GET / 호출');
    next();
}, (req, res) => {
    throw new Error('에러처리 메세지');
});

app.use((err, req, res, next) => {
    console.error(err);
    res.status(500).send(err.message);
});

app.listen(app.get('port'), () => {
    console.log(app.get('port'), '포트에서 대기중입니다.');
});
```

다른 모듈을 사용할려면 npm으로 다운받아서 require을 해야한다.
