---
layout : posts

title : "URI, URL, URN"

date : 2021-07-11

categories : web

comments : true
---



URI, URN, URL 에 대해 포스팅해볼려고 한다.

자세히 알고 있었다고 생각했었는데 막상 설명해볼려고하니 헷갈리고 어려웠다.

내가 헷갈렸던 것을 다른 독자들도 어려웠을거라고 생각하고 그 부분도 서술하였다.

<br>

### URI, URL, URN 이란

URI는 통합 자원 식별자(Uniform Resource Identifier)라고 불린다.

URI는 ID(식별자)로서의 의미가 강하며, URI에는 두가지 형태가 있는데 URL과 URN이다.

<br>

URL은 통합 자원 지시자(Uniform Resource Locator)라고 불린다.

URL은 네트워크 상에 존재하는 위치를 의미하며, 어디(WHERE)가 URL 의 핵심 개념이다.

또한 웹 사이트 주소로 알고 있지만, 주소뿐만 아니라 컴퓨터 네트워크 상의 자원을 모두 나타낼 수 있다.

특징) http, https, mailto, file, ftp 등 (Protocal 또는 Scheme)



URN은 통합 자원 이름(Uniform Resource Name)라고 불린다.

URN은 자원의 이름을 의미하며, 자원이 무엇(WHAT)인지가 핵심 개념이다.

또한 URN은 서로 중복되지 않는 유니크한 값을 가져야 한다.

URN이 나오게 된 배경은 URL 같은 경우 위치가 변경이되면 찾지못하게 되었는데, 이런 한계점을 극복하고자 나온것이 URN이다.

즉, 위치와 무관하게 리소스를 찾게 해주는 방식이다.

ex)  urn:oid:2.16.840



### URL 과 URI 차이

사실 공부하면서 가장 헷갈린것이 URL 과 URI 차이였다.

어떤 블로그에서는 URI와 URL이 같은 의미라고 서술하고 있고, 다른 블로그에서는 전혀 다른 의미라고 말하고 있어서 좀더 자세히 알아보게 되었다.

다른 블로그에서 많이 헷갈리는 만큼 필자의 글이 정확하지 않을수도 있음으로 다른 블로그들을 참고하길 바란다.

추천하는 블로그 : [URI와 URL 차이](https://velog.io/@jch9537/URI-URL)



RFC의 문서에 따르면 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986#section-3)에 있는 URI의 Scheme은 다음과 같다고 한다.

![URI](https://user-images.githubusercontent.com/66049273/125196988-e337f880-e296-11eb-94be-11174a25b60a.png)

즉 fragment 까지 포함한다고 말할수 있다.



URL 같은 경우는 [RFC1738](https://datatracker.ietf.org/doc/html/rfc1738)에 정의되어 있는데

![URL](https://user-images.githubusercontent.com/66049273/125197251-d49e1100-e297-11eb-8a11-e2d47794a80b.png)

처럼 스킴부터 쿼리파라미터까지가 URL로 정의되어 있다.



그럼 차이점은 fragment의 유무이지만 일반적으로 URL이 fragment가 포함되어져 사용되어져 왔기때문에 추후 URI를 정의할때 URI의 Scheme에 포함되었을 거라고 생각한다.
