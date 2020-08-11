---

layout : posts

title : "Nodejs REST"

date : 2020-08-11

categoris : Nodejs

comments : true

---

<h4>REST</h4>

: REpresentational State Transfer의 줄임말이며, 서버의 자원을 정의하고 자원에 대한 주소를 지정하는 방법을 가르키는 것, 일종의 약속

REST에서는 주소 외에도 HTTP 요청 메서드라는 것을 사용합니다.
- GET : 서버 자원을 가져오고자 할 때 사용합니다. 요청의 본문에 데이터를 넣지 않습니다. 데이터를 서버로 보내야 한다면 쿼리스트링을 사용합니다.
- POST : 서버에 자원을 새로 등록하고자 할 때 사용합니다. 요청의 본문에 새로 등록할 데이터를 넣어 보냅니다.
- PUT : 서버의 자원을 요청에 들어 있는 자원으로 치환하고자 할 때 사용합니다. 요청의 본문에 치환할 데이터를 넣어보냅니다.
- PATCH : 서버 자원의 일부만 수정하고자 할 때 사용합니다. 요청의 본문에 일부 수정할 데이터를 넣어 보냅니다.
- DELECT : 서버의 자원을 삭제하고자 할 때 사용합니다. 요청의 본문에 데이터를 넣지 않습니다.
- OPTIONS : 요청을 하기 전에 통신 옵션을 설명하기 위해 사용합니다.

HTTP 방식을 사용하면 클라이언트가 누구든 상관없이 같은 방식으로 서버와 소통할 수 있습니다.

이 의미는 즉 서버와 클라이언트가 분리되어있다는 소리입니다. 추후 클라리언트에 구애되지 않는다는 뜻이기도 합니다.

```javascript
const http = require('http');
const fs = require('fs').promises;

const users = {}; // 데이터 저장용

http.createServer(async (req, res) => {
  try {
    if (req.method === 'GET') {
      if (req.url === '/') {
        const data = await fs.readFile('./restFront.html');
        res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
        return res.end(data);
      } else if (req.url === '/about') {
        const data = await fs.readFile('./about.html');
        res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
        return res.end(data);
      } else if (req.url === '/users') {
        res.writeHead(201, { 'Content-Type': 'application/json; charset=utf-8' });
        return res.end(JSON.stringify(users)); // JSON를 문자열로 변환
      }
      // /도 /about도 /users도 아니면
      try {
        const data = await fs.readFile(`.${req.url}`);
        return res.end(data);
      } catch (err) {
        // 주소에 해당하는 라우트를 못 찾았다는 404 Not Found error 발생
      }
    } else if (req.method === 'POST') {
      if (req.url === '/user') {
        let body = '';
        // 요청의 body를 stream 형식으로 받음
        req.on('data', (data) => { // .push 이용시 버퍼형식으로 사용하고 end에서 문자열을 합쳐서 사용
          body += data; // 여기서 이미 스트리밍형식으로 합침
        });
        // 요청의 body를 다 받은 후 실행됨
        return req.on('end', () => {
          console.log('POST 본문(Body):', body);
          const { name } = JSON.parse(body); // 문자열을 JSON으로 변환
          // { name } : 디스럭쳐링 : body.name을 넣어준것
          const id = Date.now(); //지금시간
          users[id] = name; //인덱스값을 키:값처럼 이용한것
          res.writeHead(201, { 'Content-Type': 'text/plain; charset=utf-8' });
          res.end('ok');
        });
      }
    } else if (req.method === 'PUT') {
      if (req.url.startsWith('/user/')) {
        const key = req.url.split('/')[2]; // 문자열을 나눠서 두번째 인덱스값을 가져온다는 것
        let body = ''; // 변수 초기화
        req.on('data', (data) => {
          body += data;
        });
        return req.on('end', () => {
          console.log('PUT 본문(Body):', body);
          users[key] = JSON.parse(body).name; // 위에서 나눠서 넣은 것을 한번에 넣은 것을 보여줌.
          res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
          return res.end('ok');
        });
      }
    } else if (req.method === 'DELETE') {
      if (req.url.startsWith('/user/')) { // 앞에 문자열들이 맞다면
        const key = req.url.split('/')[2];
        delete users[key];
        res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
        return res.end('ok');
      }
    }
    res.writeHead(404); // 앞에서 아무것도 해당하지 않았을 경우 NOT FOUND에러
    return res.end('NOT FOUND');
  } catch (err) {
    console.error(err);
    res.writeHead(500, { 'Content-Type': 'text/plain; charset=utf-8' });
    res.end(err.message);
  }
})
  .listen(8082, () => {
    console.log('8082번 포트에서 서버 대기 중입니다');
  });

```  

위의 코드에 주석문을 거의다 적어놓았지만 조금더 설명을 해보겠습니다.

`req.method`로 HTTP요청 메서드를 구분하고, `req.url`로 요청주소를 구분합니다.

또 다른 HTTP요청 메소드를 사용하고싶으면 else if를 통해 사용을 하면됩니다.

res.end 앞에 return이 있는 이유는 함수를 종료시키기 위해서 입니다.

users 는 개체를 사용하여 사용자 정보를 저장했습니다.

stream으로 되어있는 데이터는 스트림 형식으로 전달되며, on을 통해 받은 데이터는 문자열이므로 JSON.parse하는 과정이 필요합니다.
