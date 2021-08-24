---
layout : posts

title : "HTTP/2 Frame과 Stream"

date : 2021-08-24

categories : java

comments : true
---



회사에서 요청할때 백엔드에서 이미 개선을 하였음에도 불구하고 아쉬운 속도를 내는 API 가 있었다. 외부 API를 이용해야 하기 때문에 API 받는 쪽 코드를 수정할 수가 없었다. 그래서 프런트 단에서 요청을 여러개로 나눠 신청하는 방법으로 개선을 하여서 속도를 줄이게 되었다.

속도를 줄일 때 HTTP/1.1의 경우 요청 응답이 하나의 묶음으로 주고받았으나 QA 서버에서 HTTP/2 버전이었기 때문에 하나의 Stream으로 하다 보니 시간이 오래 걸리게 되었고 1분이 넘어 405 Gateway timeout 에러를 받았다. http 1.1과 2버전의 차이점을 몰라서 벌어진 일이었는데 공부를 하고 나서 정리하고자 포스팅을 남긴다.

<br>

### HTTP 1.1 과 2의 차이

TTP1.1에서 HTTP 요청과 응답은 메세지라는 단위로 구성되어 있다. 메세지는 Status Line, Header와 Body 등으로 이루어져있으며 요청과 응답에 필요한 정보들을 가지고 있다. Status line은 실제로 응답에 사용된 HTTP 버전 및 RFC에 정의된 응답 코드가 있고, 응답 내용에 대한 힌트 정보가 담긴 Header, 실제 HTML 등의 Content 가 담긴 Body 부분으로 구성되어 있다.

<br>

HTTP/2 에서는 HTTP 1.1에서의 메세지라는 단위 이외에 frame, stream 이라는 단위가 추가 되었다. HTTP/2 의 구조를 이해하기 위해서는 이 세계의 기본 구조에 대한 기술적 이해가 필요하다.

- Frame : HTTP/2 통신상의 제일 작은 정보의 단위이며, Header, Data 둘중 하나이다.
- Message : HTTP/1.1 과 마찬가지로 요청 혹은 응답의 단위이며, 다수의 Frame으로 이루어진다.
- Stream : 클라이언트와 서버 사이에 맺어진 연결을 통해 양방향으로 주고 받는 하나 혹은 복수개의 Message.

<br>

즉, Frame 여러개가 모여 Message가 만들어지고, Message가 여러개 모여 Stream이 만들어진다.

<br>

### Stream

![stream](https://user-images.githubusercontent.com/66049273/130588074-7ac6b15e-fcd0-4ede-bad0-8b56f9558f50.png)

출처 : High Performance Browser Networking

<br>

다음 그림을 보면서 이해해보자. Request에서 Data frame이 없는 이유는 Get이기 때문이다. 응답을 보면 Header, Data Frame이 각각 들어있는 것을 볼수 있다. 이렇게 하나의 Stream 에서 이루어진다. Stream N 를 보면 밑의 그림처럼 양방향 통신이라서 끊기지 않고 하나의 Stream에서 존재하는 것을 볼수 있다.

<br>

### 정리

HTTP/1.1 같은 경우 요청과 응답은 각각 하나의 메세지가 하나의 단위로 요청과 응답을 했다면, HTTP/2 같은 경우는 스트림 하나가 다수개의 요청을 하게 된다. 즉, 끊기지 않고 한번에 모든 요청과 응답을 주고받는 것이다.

정리하자면 Stream 은 다른 용어에서도 유추할수 있듯이 끊김없이 연속적으로 주고받는 것이라고 생각할 수 있다.

<br>

주의할 점이라면 서버 기본 세팅 같은 경우 주고 받는 시간이 1분으로 설정되어 있다는 것이다. 1분이 넘으면 405 Gateway timeout 에러가 발생하게 되면서 원하는 값을 받지 못하게 된다. 즉, 요청과 응답을 받을때 1분이 넘지않도록 코드를 작성하는 것이 중요하다.

<br>

<br>

#### Reference

https://brunch.co.kr/@sangjinkang/3

