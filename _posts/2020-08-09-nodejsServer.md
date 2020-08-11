---

layout : posts

title : "Nodejs Server"

date : 2020-08-10

categoris : Nodejs

comments : true

---

Nodejs를 공부하면서 얻은 지식을 요약해서 정리해볼려고합니다.

서버는 클라이언트가 요청(request)을 하면 응답(response)을 해줍니다. 이것을 토대로 코드를 짜게 됩니다.

먼저 가장 뼈대를 만드는 코드입니다.

```javascript
const http = require('http');

http.createServer((req, res) => {
  //어떻게 응답할지 적는 곳
})
```

응답을 하는 코드는 res. 으로 시작하면 됩니다. 참고로 res는 매개변수이므로 바꿔도 상관 없습니다.

- `res.writeHead(HTTP상태코드, 응답에 대한 정보)` : 헤더
- `res.write(보낼 데이터)` : 본문

**HTTP상태코드**
- 2XX : 성공을 알리는 상태 코드, 200(성공), 201(작성됨)이 많이 상용됨.
- 3XX : 리다이렉션(다른 페이지 이동)을 알리는 상태코드,301(영구이동), 302(임시이동), 304(수정되지 않음)이 대표적입니다.
- 4XX : 요청 오류를 뜻합니다. 대표적으로 400(잘못된 요청), 401(권한없음), 403(금지됨), 404(찾을 수 없음)이 있습니다.
- 5XX : 서버 오류를 나타냅니다. 예기치 못한 에러발생 시 발생, 500(내부서버 오류), 502(불량 게이트웨이), 503(서비스를 사용할 수 없음)

나머지는 코드를 보시면서 설명하겠습니다.

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
  res.write('<h1>Hello Node!</h1>');
  res.end('<p>Hello Server!</p>');
});
server.listen(8080);

server.on('listening', () => {
  console.log('8080번 포트에서 서버 대기 중입니다!');
});
server.on('error', (error) => {
  console.error(error);
});
```

헤더부분에 응답에 대한 정보는 콘텐츠 형식, 한글을 위해 인코딩방식을 정해주었습니다.

참고) 이미 사용하고있는 포트번호이면 EADDRINUSE 에러가 발생합니다.

이런 경우 포트번호를 바꿔주거나 사용중인 프로세스를 꺼주시면 됩니다.

오류에 대비 + HTML을 불러와보겠습니다.

```javascript
const http = require('http');
const fs = require('fs').promises;

http.createServer(async (req, res) => {
  try {
    const data = await fs.readFile('./server2.html');
    res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end(data);
  } catch (err) {
    console.error(err);
    res.writeHead(500, { 'Content-Type': 'text/plain; charset=utf-8' });
    res.end(err.message);
  }
})
  .listen(8081, () => {
    console.log('8081번 포트에서 서버 대기 중입니다!');
  });
```

res.end는 catch부분에도 꼭 써주셔야됩니다. 클라이언트는 서버로부터 응답이 오길 기다리다가 timeout(시간초과) 처리합니다.

오류를 위해 try, catch를 써주셔서 오류를 잡아주셔야합니다.
